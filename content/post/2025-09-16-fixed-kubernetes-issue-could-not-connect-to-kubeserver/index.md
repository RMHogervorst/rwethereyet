---
title: Fixed Kubernetes Issue, Could not Connect to Kubeserver
author: Roel M. Hogervorst
date: '2025-09-16'
slug: fixed-kubernetes-issue-could-not-connect-to-kubeserver
categories:
  - blog
tags:
  - lessons-learned
  - kubernetes
difficulty:
  - beginner
---

Small learning, I could not connect to my kubernetes cluster. I downloaded the 
kubeconfig file (~/.kube/config) from the kubernetes cluster. I had to modify it, because it pointed
to localhost (127.0.0.1).

```yaml
apiVersion: v1
clusters:
  - cluster:
      certificate-authority-data: ...
      server: NAMEHERE
    name: default
[...]
```
Here is what I did wrong: I used a DNS name (kubernetes.local:6443) instead of an ip-address.

Took me a long time to figure out that I needed an ip address here.
