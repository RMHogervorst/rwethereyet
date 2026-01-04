---
title: Fun with Certificates, Containers in Corporate Networks
author: Roel M. Hogervorst
date: '2025-09-18'
slug: fun-with-certificates-containers-in-corporate-networks
categories:
  - blog
tags:
  - kubernetes
  - certificate
difficulty:
  - advanced
post-type:
  - walkthrough
subtitle: ''
---

_(I republished this post  on my main blog: [blog.rmhogervorst.nl](https://blog.rmhogervorst.nl/blog/2025/08/02/hacking-etc-ssl-certs-with-containers-in-corporate-networks/))_
As a consultant I come into different organizations, usually of the larger size.  
Making my custom applications work in those orgs often revolves around wrangling with TLS certificates.

I found a way to make premade containers in kubernetes trust self-signed certificates without rebuilding the container by mounting a configMap.

## A detour into TLS, certificates and trust
Almost all the websites in the world use TLS[^2] (transport layer security). It works with certificates, cryptographically signed documents that tell the browser (or your app) that the website they are visiting is in fact that website. 
How does your browser determine that that is true? The browser checks the certificate against a list of known 'safe' certificates in a root-store; if that certificate is in the root store of the device or root store of the browser the certificate checks out and the connection is allowed. That never happens. There are currently 148 certificates in my root store on this ubuntu machine.

If the certificate is not in the store, a chain of certificates is followed until a certificate is found that matches one in the root store. Because every certificate is signed by another certificate.  That certificate is signed by another and so on. In practice a certificate authority has one root cert that is kept very private, that certificate is used to sign intermediate certificates, those are then used to sign others and finally one of those certificates is used to sign certificates of websites[^1]. So my browser sees a certificate that signs the blog.rmhogervorst.nl website, that certificate comes from letsencrypt and is signed by an E6 certificate (which is also from letsencrypt) and that one is signed by ISRG Root X1. which is in my root store

[^1]: I know, I know, signing a certificate with a certificate is not correct. There are keys involved and PEMs and restrictions on what a key can sign and what not, and there are specific periods when keys/certs are valid. But I don't really want to explain all of that just because I found a cool trick. Certs signing certs are lies we tell children, until they are ready to learn more.
[^2]: It was called SSL before, I am not just saying that to sound smart and senior, but to help you find this website if you searched for SSL certificate, in stead of TLS certificate.

Okay, what the hell, why this whole paragraph about certificates? Because massive organizations
often use self-signed certificates. They sign their websites with certificates that are not in the standard root store
of your browser. But since the companies also control the laptops of their employees they can install
those certificates into their laptops. Some massive organisations even terminate
all the tls connections from outside at their firewall, and re-encrypt the
pages with their own tls certificate. That way they can inspect the traffic, do
caching and have full insight into the network traffic in the network[^3]. ALL the
traffic in the network now uses the same root certificate.


[^3]: Yeah that is massive 'spying' on your own network, but organizations want to know when the cryptominer was deployed, and who downloaded the malware the first time. I understand the usecase.

But if I build a container for my services, it is based on standard ubuntu or python containers.
Those containers do not have the root certificate of the org. And so any https call my process makes to websites of the org will break
because the TLS connection is not trusted.
Luckily there is well known process to add new root certificates to ubuntu.
You place your certificate in `/usr/local/share/ca-certificates`, you run the `sudo update-ca-certificates` command and the root store trusts your certificate.
easy.

## Bypassing update-ca-certificates in ubuntu entirely

If you build a container you can do the above in one of the first steps of the dockerfile. If you have a python process you can skip this step entirely and place the certificate somewhere convenient and use env vars to let the process know where to find the certificate.
But, if you have a premade container that does a curl call to a corporate TLS encrypted service with a corporate certificate, you don't need to rebuild that container, you can tweak your kubernetes configuration to make it work. _Finally! I'm getting to a point!_

### what does update-ca-certificates do?
the `update-ca-certificates` command is actually a shell script (in /usr/sbin/update-ca-certificates) that does a lot of things. 
- it takes the new certificate that ends in `.crt` and creates a symlink in /etc/ssl/certs/ with filename.pem
- it appends the certificate to the file `/etc/ssl/certs/ca-certificates`
- it creates a hash of the certificate  with `OPENSSL x509 -hash -fingerprint` and creates a symlink in /etc/ssl/certs with the name `[hash].0` unless there already is a file with that hash, than it increments the number.  (These files are used by curl to quickly compare certs based on hash, quite cool actually)

### Trust only one certificate

Here is what I realized: you only need to trust **one** certificate, all the others are not relevant.
So you only need THAT certificate in the store. In kubernetes you can replace a directory with a configMap. What if we did the `update-ca-certificates` work ourselves on only the certificate that we need, but without all the other certificates. 

So we add the certificate twice, once under the name `ca-certificates` and once under the name `[hash].0`.

```yaml
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: certs
data:
	# this is an example, your certificate looks different and will have a different hash
    ca-certificates: |
	    -----BEGIN CERTIFICATE-----
		MIIDazCCAlOgAwIBAgIUKSwhLqUWcb/9OWLDSa8AYrqLIoswDQYJKoZIhvcNAQEL
		BQAwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgMClNvbWUtU3RhdGUxITAfBgNVBAoM
		[...]
		fcbORe+ZcVJSfH9XD9gs
		-----END CERTIFICATE-----
	9da13359.0: |
		-----BEGIN CERTIFICATE-----
		MIIDazCCAlOgAwIBAgIUKSwhLqUWcb/9OWLDSa8AYrqLIoswDQYJKoZIhvcNAQEL
		BQAwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgMClNvbWUtU3RhdGUxITAfBgNVBAoM
		[...]
		fcbORe+ZcVJSfH9XD9gs
		-----END CERTIFICATE-----
```

We can than mount this configMap inside the pod.

```yaml
[...]
    spec:
      containers:
      - name: containername
        image: containerimage:5634529
        env:
        # if you use python you need to set this anyways
        - name: REQUESTS_CA_BUNDLE
          value: /etc/ssl/certs
	    [...]
		volumeMounts:
        - name: certificates
          mountPath: /etc/ssl/certs
      volumes:
      - name: certificates 
        configMap:
          name: certs
[...]
```

When the pod starts up it will replace the /etc/ssl/certs directory with 2 files (`ca-certificates` and `9da13359.0`). And the system will trust your corporate certificate! 

Is this better than other ways? I don't know, I thought it was elegant and hacky at the same time.

### Notes and alternatives

I got the inspiration from a stackoverflow post that I cannot find back.
If you use curl, you can also add the cert somewhere in the container (mounting that configMap to a place of your choice) and use an env-var CURL_CA_BUNDLE to point curl to the right place.
If you use python you can do something similar with REQUESTS_CA_BUNDLE. In fact you NEED to set this variable either way because python defaults to a `certify` package that contains the root certificates of browsers and so this cool hack will be less effective. That is why I added the env var in the example.

Read more:
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/
- https://documentation.ubuntu.com/server/how-to/security/install-a-root-ca-certificate-in-the-trust-store/

