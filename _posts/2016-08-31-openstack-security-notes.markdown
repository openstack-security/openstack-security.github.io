---
layout: post
title:  "OpenStack Security Notes"
date:   2016-08-31
categories: security-notes
tags: security notes vulnerabilities
author: "lhinds @ Red Hat"
---

In this post I will explain what OpenStack Security notes are, and how they
benefit OpenStack operators.

Recently tmcpeak and sicare provided a roundup of the [OpenStack Vulnerability
Management process](http://openstack-security.github.io/vulnerabilities/2016/05/05/clearing-the-air.html)
, if you did not get a chance to read this blog, grab the opportunity and then
return here, as OpenStack Notes are the sister process and also a key part of
how OpenStack manages security risks.

OpenStack Security Notes (OSSNs) are security notifications which let operators 
know of a newly identified risks and the steps they should take to mitigate that 
issue. In many cases, OSSNs are used to publicise issues which cannot be fixed 
with a code patch to openstack and instead make recommendations to resolve the 
issue with compensating controls, such as architectural or configuration changes.

OSSN’s are born out of a vulnerability report. It is often decided within the 
discussion of a launchpad security bug, that a security advisory should be made 
to the community, to ensure a clear understanding is communicated of the nature 
any given security risk.

Some examples of recent OSSN’s are:

[Bandit versions lower than 1.1.0 do not escape HTML in issue reports](https://wiki.openstack.org/wiki/OSSN/OSSN-0070)

[Repeated token revocation requests, can lead to service degradation or disruption](https://wiki.openstack.org/wiki/OSSN/OSSN-0068)

[Barbican server discloses SQL Connection String and X-auth token](https://wiki.openstack.org/wiki/OSSN/OSSN-0067)

The end to end process of an OSSN, starts when a member of the security group,
a project core, or a VMT member, marks a launchpad bug as an
‘OpenStack Security Note’. Shortly after this, an author will then assign
themselves to the bug, and get to work on authoring the OSSN.

Once the author has a draft in place, they will submit a patch to the
security-docs repo, where other members of the security group, and cores from
the related project of the OSSN, will provide reviews on the patch / draft.

After the patch has received two +2 reviews from security group core members,
and a +1 from a core within the related project, the OSSN is merged into the
security-docs repo.

Shortly after merge, the reviewed text will be posted to the [OpenStack Wiki](https://wiki.openstack.org/wiki/OSSN)
, and a GPG signed [email](http://lists.openstack.org/pipermail/openstack-dev/2016-July/099776.html)
will be sent to the main openstack & openstack-dev mailing lists.

The OpenStack Security Group welcomes anyone who wants to Author or help review
OSSN’s.

OSSN’s are very good way of introducing yourself to security related work in
OpenStack. It allows you to learn the complete gerrit workflow, and gains you
valuable experience in how specs and documentation is accepted within the
OpenStack community. They also gain credit for your organization's focus on 
security.

We also welcome feedback from Operators on how valuable you find OSSN's, and
ways you feel may improve the process.

The OpenStack Security Group can be found on are irc-channel #openstack-security
and we meet weekly on #openstack-meeting-alt every Thursday @ 17:00 UTC time.

You can also email the group, on our [mailing list](http://lists.openstack.org/cgi-bin/mailman/listinfo/openstack-security)
