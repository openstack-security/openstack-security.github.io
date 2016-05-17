---
layout: post
title:  "Clearing the Air about Vulnerabilities in OpenStack"
date:   2016-05-05
categories: vulnerabilities
tags: security vmt vulnerabilities summit
author: "tmcpeak @ IBM Cloud, sicarie @ HPE"
---

Recently, there have been a few talks around "vulnerabilities" within
the OpenStack project that introduced some unfair concern.

Some of them call out important concepts such as
[CIA](https://en.wikipedia.org/wiki/Information_security#Key_concepts)
and the [CVE database](https://cve.mitre.org/). Unfortunately, they all
attempt to highlight vulnerabilities or attack vectors within OpenStack
that have either been addressed years ago, or are not able to be addressed
by the upstream community and are the responsibility of the group
deploying and maintaining the cloud.

To understand how OpenStack handles vulnerabilities securely, it is
important to briefly introduce the OpenStack vulnerability management
process.

## Vulnerability Management in OpenStack
A vulnerability in OpenStack usually begins life as a bug filed against
a project with the "security" tag.  These bugs are marked private and sent
directly to the project's security team and the Vulnerability Management Team
(VMT). An initial triage is performed to understand whether the bug represents
a legitimate security issue and if so what the impact is.  If the issue is
confirmed, an advisory and patch are prepared and validated privately.
Once the the advisory and fix are available, OpenStack stakeholders are
given two weeks early notice to patch their systems before public disclosure.
The reason the two week notice is important is because **it is expected that
a responsible OpenStack provider will respond to security advisories in a
timely manner.**

![VMT Process](https://security.openstack.org/_images/vmt-process.png)


## Vulnerability Management Outside of OpenStack
The Vulnerability Management Team (VMT) only manages issues for OpenStack
components (with the "vulnerability:managed" tag) inside the OpenStack ecosystem.
A portion of recently discussed "vulnerabilities" have to do with third party
applications deployed on an OpenStack cloud. The responsibility for securing
third party applications is shared between the third party developer to produce
timely patches to secure products, distributions to make sure there are sane
defaults baked-in to the product, deployers to ensure their configurations are
tuned to their environment and applications as well as patching methods, and
the OpenStack community. To that end, the OpenStack Security Project maintains
the [OpenStack Security Guide](http://docs.openstack.org/security-guide/) for
help architecting secure environments, and [Security Notes](https://wiki.openstack.org/wiki/Security_Notes)
to address common deployment-specific issues that have been found.


## Conclusion - We're Here To Help
The OpenStack community is very concerned about security, and actively engages
the upstream community, deployers, and operators to help increase the overall
security posture of every OpenStack deployment. The Security Project has
released many tools and references to assist everyone with the knowledge to
securely configure and maintain their OpenStack cloud.

Finally, if you have found a security issue in OpenStack, please disclose it
responsibly by marking "security" in the LaunchPad bug report, or by contacting
the involved project team or VMT team members directly. The Security Project
welcomes everyone wishing to discuss, learn, or contribute to the security of
the OpenStack project and can be found on freenode in the #openstack-security
room, or on the OpenStack developers mailinglist with the [security] tag.
