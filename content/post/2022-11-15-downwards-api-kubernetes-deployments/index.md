---
title: Downwards Api Kubernetes Deployments, environmental variables 
author: Roel M. Hogervorst
date: '2022-11-15'
slug: downwards-api-kubernetes-deployments
categories:
  - blog
tags:
  - kubernetes
  - yaml
  - environmental variables
difficulty:
  - advanced
post-type:
  - lessons-learned
subtitle: 'check the logs before you scream'
---

A very technical thing that I don't want to look up again.

If you work with kubernetes and want to expose information about the pod and
the machine that the container is running on to the program inside the container
you need to pass that information down. This is called the downward-api[^2] in 
kubernetes. 

The idea behind kubernetes is that you don't have to care about the underlying
hardware, it is an abstraction on top of that. But in practice you want to 
spot if your failing pods all fail on the same node.

So how do you do it.

Your program lives inside a container.
That container lives inside a pod.
that pod is often deployed in a control structure such as a 'deployment'
that lives inside a namespace.

```
namespace
    deployment/job/whatever
        pod
            container
                program
```

According to the documentation[^1] you can add an environmental variable like this

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dapi-envars-fieldref
spec:
  containers:
    - name: test-container
      image: registry.k8s.io/busybox
      command: [ "sh", "-c"]
      args:
      - while true; do
          echo -en '\n';
          printenv MY_NODE_NAME MY_POD_NAME MY_POD_NAMESPACE;
          printenv MY_POD_IP MY_POD_SERVICE_ACCOUNT;
          sleep 10;
        done;
      env:
        - name: MY_NODE_NAME
          valueFrom:
            fieldRef:
              fieldPath: spec.nodeName

```
Note that this is a description for a pod. So you have to modify this 
to make a deployment but when I created this in a deployment I couldn't see the MY_NODE_NAME env var in the yaml of the pod. So I thought it wasn't working.


But when you check the logs you see that the env var is correct. 

My mistake was that I didn't check the logs. A deployment doesn't know where
or when the pod will be created, only at runtime are the variables like
nodename available. 



[^1]: <https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information/>
[^2]:https://kubernetes.io/docs/concepts/workloads/pods/downward-api/
