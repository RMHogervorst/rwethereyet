---
title: Cgroups Syscalls Namespaces, all the Components of Kubernetes (Linkpost)
author: Roel M. Hogervorst
date: '2025-09-17'
slug: cgroups-syscalls-namespaces-all-the-components-of-kubernetes-linkpost
categories:
  - blog
tags:
  - kubernetes
difficulty:
  - advanced
post-type:
  - link
subtitle: 'k8s is just linux'
---

This is a great explainer for the components of kubernetes/docker:
it talks about cgroups (that limit what a container can do), syscalls (that you can limit on a container in kubernetes)
and so much more. 

<https://learnkube.com/security-contexts>

Dave Altena really shows that kubernetes is 'just linux' but scaled over
several machines.
If you want some insight in the how and what of security context in kubernetes
this is the post.

Find other linkposts [here](https://notes.rmhogervorst.nl/post-type/link/)
