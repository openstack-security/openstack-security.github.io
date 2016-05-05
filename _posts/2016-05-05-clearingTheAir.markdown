---
layout: post
title:  "Clearing the Air about Vulnerabilities in OpenStack"
date:   2016-05-05
categories: vulnerabilities
tags: security vmt vulnerabilities summit
author: "tmcpeak @ IBM Cloud, sicarie @ HPE"
---
I recently came across a vBrownBag talk from the 2016 Austin summit
called ["Security Vulnerabilities in OpenStack deployments"](https://www.youtube.com/watch?v=twOC6OqXBAU)
that got me thinking it might be a good time to address vulnerabilities in
OpenStack, as well as provide a brief overview of how they are handled and
the responsibilities of an OpenStack deployer.

I'll start by noting that I mostly enjoyed this talk.  Ravi does a
good job of introducing some important concepts such as [CIA](https://en.wikipedia.org/wiki/Information_security#Key_concepts)
and the [CVE database](https://cve.mitre.org/).  The sticking point for
me is the claim: "Lately I've been able to completely take control of
the OpenStack cloud when somebody deploys it."  This claim is substantiated
with three <sup>1,2,3</sup> example issues, but the referenced issues aren't sufficient
to compromise any responsibly deployed OpenStack cloud.

To understand why, it's important to briefly introduce the OpenStack
vulnerability management process.

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

The vulnerability management team only manages issues for OpenStack components,
so while the the first mentioned issue <sup>1</sup> (an issue in OpenStack
Neutron) generated an advisory <sup>4</sup>, the third issue <sup>3</sup> (an issue
in PostgreSQL) did not because it's in a third party component.  
This  brings us to another key point: **it is expected that a responsible
OpenStack provider will keep infrastructure updated by performing regular
package updates as provided by their operating system distribution.**

## Conclusion
Ravi seems very knowledgable and passionate about security.  I hope he will
continue to participate in security to make OpenStack more secure for all.  

Deployers should follow all guidance mentioned in the
[OpenStack Security Guide](http://docs.openstack.org/security-guide/) and
always keep systems up to date.  The OpenStack Security Project also makes
[Security Notes](https://wiki.openstack.org/wiki/Security_Notes) available to
provide quick security guidance to deployers.

Finally if you have found a
security issue in OpenStack, please disclose it responsibly by marking
"security" in the LaunchPad bug report, or by contacting the involved project
team members directly.

<sup>1</sup>[CVE-2014-0187](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0187)

<sup>2</sup>[CVE-2015-8557](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-8557)

<sup>3</sup>[CVE-2016-0766](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0766)

<sup>4</sup>[OSSA-2014-014](https://security.openstack.org/ossa/OSSA-2014-014.html)
