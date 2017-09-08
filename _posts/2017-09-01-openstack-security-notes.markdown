---
layout: post
title:  "OpenStack Security Notes, and how they help you the Operator"
date:   2017-09-08
categories: security-notes
tags: security notes vulnerabilities
author: "lhinds @ Red Hat"
---

For this post I will explain what OpenStack Security notes are, and how
they benefit operators in securing an OpenStack Cloud.

OpenStack Security Notes (OSSN's) are solely to notify operators of a
discovered risk, that are often not directly addressed by a code patch.

OSSN's can be in the form of a deployment architecture recommendation,
configuration value or a file permission.

Consider the meme 'If you do this, you're going to have a bad time' to
get an idea of what OSSN's are about.

Some examples of recent OSSN's would be:

- [Ceph credentials included in logs using older versions of libvirt/qemu](https://wiki.openstack.org/wiki/OSSN/OSSN-0079)

- [copy_from in Image Service API v1 allows network port scan](https://wiki.openstack.org/wiki/OSSN/OSSN-0078)

- [Glance Image service v1 and v2 api image-create vulnerability](https://wiki.openstack.org/wiki/OSSN/OSSN-0076)

The end to end process of an OSSN, starts when a member of the security
project, a project core, or a VMT member, mark a launchpad bug by adding
the ‘OpenStack Security Note’  group. An author will then assign
themselves to the bug, and will commit to authoring the OSSN. Public
notes may be worked on by anyone, whereas embargoed notes are only
handled by the security project core members.

Once the author has a draft in place, they will submit a patch to the
[security-docs repo](https://review.openstack.org/#/admin/projects/openstack/security-doc),
where other members of the security project and cores from the related
project of the original launchpad bug, can review the note content.

After the patch has received two +2 reviews from security project core
members, and a +1 from a core within the concerned project, the OSSN is
merged into the security-docs repository.

Once merged, the reviewed text will be posted to the [OpenStack Wiki](https://wiki.openstack.org/wiki/OSSN)
, and a GPG signed email will be sent to the [openstack](http://lists.openstack.org/cgi-bin/mailman/listinfo/openstack) & [openstack-dev](http://lists.openstack.org/cgi-bin/mailman/listinfo/openstack-dev) mailing lists.

The OpenStack Security Project welcomes anyone who wants to help Author
or review OSSN's. Security Notes are often a path to the election of
core members of the OpenStack security project. OSSN authorship was how
I personally found myself elected almost two years back.

Anyone new to the security project offering to help author a Security
Note, will be given lots of support on creating their first OSSN from
other Security Project members.

We also welcome feedback from operators on how valuable you find OSSN's,
and ways you feel may improve the process. After all, the process is
there to benefit you the operator.

For anyone with an interest in OpenStack Security, the OpenStack
Security Project can be found on the irc-channel #openstack-security and
we meet weekly on #openstack-meeting-alt every Thursday @ 17:00 UTC time.

You can also email the security project on the OpenStack developer mailing
list, by using a [security] tag in the subject line.

Luke Hinds (Security Project PTL)
