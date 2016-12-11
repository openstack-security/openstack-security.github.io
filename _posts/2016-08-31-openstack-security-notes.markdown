---
layout: post
title:  "OpenStack Security Notes"
date:   2016-08-31
categories: security-notes
tags: security notes vulnerabilities
author: "lhinds @ Red Hat"
---

<<<<<<< HEAD
For this post I will explain what OpenStack Security notes are, and how they
benefit OpenStack operators.

Recently Travis Mcpeak and Nathaniel Dillon (sicaire) provided a roundup of the [OpenStack Vulnerability
=======
In this post I will explain what OpenStack Security notes are, and how they
benefit OpenStack operators.

Recently tmcpeak and sicare provided a roundup of the [OpenStack Vulnerability
>>>>>>> d00831e37ca97391ed6a4ccd74b18d518ad065f0
Management process](http://openstack-security.github.io/vulnerabilities/2016/05/05/clearing-the-air.html)
, if you did not get a chance to read this blog, grab the opportunity and then
return here, as OpenStack Notes are the sister process and also a key part of
how OpenStack manages security risks.

<<<<<<< HEAD
OpenStack Security Notes (OSSNs), are security notifications that are generated
to notify operators of a discovered risk, that are often not (but not always)
directly addressed by a code patch. OSSN's can be in the form of a deployment
architecture recommendation, configuration value or a file permission.

OSSNs are often born out of a vulnerability. The decision to issue an OSSN happens 
as part of the discussion of a security bug on LaunchPad. The OSSN is written to 
communicate clearly the nature of the security issue.

Some examples of recent OSSNs would be:

- [Host machine exposed to tenant networks via IPv6](https://wiki.openstack.org/w/index.php?title=OSSN/OSSN-0069)

- [Bandit versions lower than 1.1.0 do not escape HTML in issue reports](https://wiki.openstack.org/wiki/OSSN/OSSN-0070)

- [Repeated token revocation requests, can lead to service degradation or disruption](https://wiki.openstack.org/wiki/OSSN/OSSN-0068)

The end to end process of an OSSN, starts when a member of the security project,
a project core, or a VMT member, mark a launchpad bug by adding the
‘OpenStack Security Note’ launchpad group. An author will then assign
themselves to the bug, and will commit to authoring the OSSN. Public notes may
be worked on by anyone, whereas embargoed notes are only handled by the security
project core members. 

Once the author has a draft in place, they will submit a patch to the
[security-docs repo](https://review.openstack.org/#/admin/projects/openstack/security-doc), where other members of the security project, and cores from
the related project of the OSSN, will provide feedback on the review.

After the patch has received two +2 reviews from security project core members,
=======
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
>>>>>>> d00831e37ca97391ed6a4ccd74b18d518ad065f0
and a +1 from a core within the related project, the OSSN is merged into the
security-docs repo.

Shortly after merge, the reviewed text will be posted to the [OpenStack Wiki](https://wiki.openstack.org/wiki/OSSN)
<<<<<<< HEAD
, and a GPG signed email will be sent to the main [openstack](http://lists.openstack.org/cgi-bin/mailman/listinfo/openstack) & [openstack-dev](http://lists.openstack.org/cgi-bin/mailman/listinfo/openstack-dev) mailing lists.

The OpenStack Security Project welcomes anyone who wants to Author or help review
OSSNs.

OSSNs are very good way of introducing yourself to security related work in
OpenStack. It allows you to learn the complete gerrit workflow, and gains you
valuable experience in how specs and documentation is accepted within the
OpenStack community.

We also welcome feedback from operators on how valuable you find OSSNs, and
ways you feel may improve the process.

The OpenStack Security Project can be found on are irc-channel #openstack-security
and we meet weekly on #openstack-meeting-alt every Thursday @ 17:00 UTC time. 

An archive of previous meetings can be found on [eavesdrop](http://eavesdrop.openstack.org/meetings/security/).

You can also email the security project, on OpenStack developer mailing list, 
by using the [security] tag in the subject line. 
=======
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
>>>>>>> d00831e37ca97391ed6a4ccd74b18d518ad065f0
