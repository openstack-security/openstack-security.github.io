---
layout: post
title:  "Clearing the Air about Vulnerabilities in OpenStack"
date:   2016-05-05
categories: vulnerabilities
tags: security vmt vulnerabilities summit
author: "tmcpeak @ IBM Cloud, sicarie @ HPE"
---

Recently, there have been a few talks around "vulnerabilities" within
the OpenStack project that missed the mark so much they deserve note.

While some of them call out important concepts such as
[CIA](https://en.wikipedia.org/wiki/Information_security#Key_concepts)
and the [CVE database](https://cve.mitre.org/), they all attempt to
highlight vulnerabilities or attack vectors within OpenStack that
have either been addressed years ago, or are not able to be addressed
by the upstream community and are the responsibility of the group
deploying and maintaining the cloud.

To understand why upstream OpenStack `is` secure, it's important to
briefly introduce the OpenStack vulnerability management process.

## Vulnerability Management in OpenStack
A vulnerability in OpenStack usually begins life as a bug filed against
a project with the "security" tag.  These bugs are marked private and sent
directly to the project's security team and the VMT.  An initial triage is
performed to understand whether the bug represents a legitimate security issue
and if so what the impact is.  If the issue is confirmed, an advisory and patch
are prepared and validated privately.  Once the the advisory and fix are
available, OpenStack stakeholders are given two weeks early notice to patch
their systems before public disclosure.  The reason the two week notice is
important is because **it is expected that a responsible OpenStack provider
will respond to security advisories in a timely manner.**

![VMT Process](https://security.openstack.org/_images/vmt-process.png)


## Vulnerability Management Outside of OpenStack
The Vulnerability Management Team (VMT) only manages issues for OpenStack
componens (with the "vulnerability:managed" tag) inside the OpenStack ecosystem.
A large part of other claimed "vulnerabilities" have to do with third party
applications deployed on an OpenStack cloud. Unfortunately, much as an
operating system is utilized to host insecure things like old versions of
Java or PHP that can be vulnerable to many attacks, so OpenStack is used to
host applications that can also be vulnerable. It is the responsibility of
the group maintaining and distributing the third party application to managed
the security of that application (ie, a vulnerability in PostGRE SQL is `not`
a vulnerability within OpenStack).


## Conclusion - Please Deploy Things Securely
Finally, it is up to the individual group deploying and maintaining the
OpenStack cloud to do so in a secure fashion. The recommendations mentioned in the
[OpenStack Security Guide](http://docs.openstack.org/security-guide/) are
frequently summarized with checklists to help deployers stand up a service
securely.  Additionally, the OpenStack Security Project also makes
[Security Notes](https://wiki.openstack.org/wiki/Security_Notes) available to
provide quick security guidance to deployers.

Finally, if you have found a security issue in OpenStack, please disclose it
responsibly by marking "security" in the LaunchPad bug report, or by contacting
the involved project team or VMT team members directly.
