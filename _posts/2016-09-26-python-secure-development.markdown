---
layout: post
title:  "Secure Development in Python"
date:   2016-09-26
categories: Organization
tags: OSSP Python Security
author: "tmcpeak @ IBM Cloud"
---

OpenStack is one of the largest Python projects, both in code size and
number of contributors.  Like any development language, Python has a set of best
(and worst) security practices that developers should be aware of to avoid common
security pitfalls.  One mission of the OpenStack Security Project is to help
developers write Python code as securely and easily as possible, so we created two
resources to help.

## Secure Development Guidelines
![Easy](https://openstack-security.github.io/assets/make_it_easy.jpg)

The [Secure Development Guidelines](https://security.openstack.org/#secure-development-guidelines)
were created with the goal to make it quick and easy for a developer to learn:
- What is the best practice
- An example of the incorrect (insecure!) way of accomplishing a task
- An example of the correct way of accomplishing a task
- Consequences for not following best practices
- Links for further Reference

As developers ourselves we're guilty of more than the occasional copy-paste.  The
`Correct` section of the `Secure Development Guidelines` are a perfect source to jump
in and get the best practice code snippet you need.

## Bandit
[Bandit](https://wiki.openstack.org/wiki/Security/Projects/Bandit) was built to find
common insecure coding practices in Python code.  Developed for the OpenStack
community by the OSSP, it is the best Python static analysis tool available
(in our biased opinion).  Like all OSSP resources and tools, Bandit is open
source and we encourage people to use it, extend it, and provide feedback.

If you're new to Bandit a good way to get started is by watching this:
[![presentation](https://img.youtube.com/vi/hxbbpdUdU_k/0.jpg)](https://www.youtube.com/watch?v=hxbbpdUdU_k "Securing the OpenStack code base with Bandit")

Also check out our [wiki](https://wiki.openstack.org/wiki/Security/Projects/Bandit).

If you have any questions please contact us on the OpenStack Developer Mailing list
(using the [Security] tag), or visit us on IRC in `#openstack-security` on Freenode.
