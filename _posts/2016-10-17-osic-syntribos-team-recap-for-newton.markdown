---
layout: post
title:  "Syntribos team recap for Newton"
date:   2016-10-17
categories: syntribos
tags: OSSP Python Security Syntribos
author: "cneill @ Rackspace"
---

Our team set out to accomplish several tasks during the Newton cycle:

- Improve [Syntribos][] to the point that it was reliable and useful
  for testing the 6 projects [OSIC][] has chosen to focus on for Newton
  ([keystone][], [neutron][], [glance][], [nova][], [cinder][], and [swift][])
- Test those 6 key projects and report our results to upstream developers
- Based on our results, determine future action items to further improve
  Syntribos

We succeeded in making Syntribos more configurable, easier to use, and less
prone to false positives. We released several new features, removed cruft
in the codebase, added function/class comments, and wrote unit tests, all with
the goal of making Syntribos a more effective tool for testers, and easier
to contribute to as a developer. We were able to test all 6 key projects, and
reported several bugs in their Launchpads.

We started off the cycle by making improvements aimed at easing further
development. This included cleaning up the codebase, creating documentation with
sphinx, fixing bugs, writing unit tests, and adding docstrings, among other
changes. We also removed our dependency on OpenCAFE at the request of some in
the community, which took several weeks. This leaves us with a pretty small
dependency base, which should make future maintenance / modification more
manageable. Once we were more confident in the core codebase, we started
focusing on how to improve the accuracy and depth of tests conducted by
Syntribos. We used a special vulnerable API created by Matt Valdes from
Rackspace to validate our improvements, and ensure that our tests were detecting
the issues we introduced into the API.

We spent a significant amount of time creating templates and extensions for each
project. This typically took at least 1 or 2 days per project, significantly
reducing the amount of time we spent testing. However, much of the heavy legwork
for testing these projects is now out of the way, and future testing should
be significantly easier. Our team is also more experienced with the OpenStack
projects we tested, and with security testing in general in some cases.

Overall, we believe we were successful in meeting our goals for this cycle,
though we believe that more work is required to get Syntribos ready for
production use by others in the community.

Our Key Accomplishments
=======================

- Worked to improve Syntribos tool from April 5th through September 30th
- Participated in the OpenStack Security Project's midcycle, where we wrote
  several OSSNs, contributed to the barbican threat analysis process, and
  discussed Syntribos with others in the community
- Tested 6 OSIC key projects from August 29th through September 30th
- Found 4 defects during our testing, and submitted them in projects' Launchpads

Metrics
=======

Syntribos
---------

- Bugs reported in Launchpad: **17** [[3]]
- Bugs resolved: **15** [[3]]
- Unit test coverage at start: **9%**
- Unit test coverage at end: **63%**

OSIC Key Projects
-----------------

- Request templates created: **611** [[4]]
- Bugs reported in Launchpad: **4** (see [Reported Bugs](#reported-bugs) below)

Reported Bugs
=============

- **String "..%c0%af" causes 500 errors in multiple locations**
    - Affects: keystone, cinder, neutron, glance
    - Launchpad: https://bugs.launchpad.net/keystone/+bug/1613901

- **[Duplicate] Stored XSS in glance image names**
    - Affects: horizon
    - Launchpad: https://bugs.launchpad.net/horizon/+bug/1623735

- **Authenticated "billion laughs" memory exhaustion / DoS in ovf_process.py**
    - Affects: glance
    - Launchpad: https://bugs.launchpad.net/glance/+bug/1625402

- One embargoed issue that is still being triaged

Challenges
==========

- Removing OpenCAFE took several weeks, and while it removed a large dependency,
  it cut down on time for other improvements.
- Our short testing schedule (1 month of testing for 6 projects) didn't give
  us much time to learn the intricacies of each project, and test them at a
  deeper, domain-specific level. Some projects offered significantly more
  endpoints than others, and in some cases we had to move on before fully
  evaluating every component. However, we were able to at least do some basic
  testing on every offered endpoint for every tested service.
    - The significant time investment required to create templates for each
      project further limited the time we had to test these projects.
- Lack of unit tests meant that many changes introduced bugs/crashes into
  master and required fix-ups. This happened less often as our coverage
  improved.
- Documentation was lacking or inaccurate at the outset, and required
  significant effort to improve.
- Our team's relative inexperience with the OpenStack projects under test, and
  security testing in general in some cases, made testing more challenging.
Syntribos Improvements / Future Plans
=====================================

As we performed our one-month engagement testing various OpenStack services,
several members of the team [took notes](https://etherpad.openstack.org/p/syntribos-future)
about features, bugs, and general improvements to be made in Syntribos.

Planned Changes for Ocata
-------------------------

- Cutting a stable Syntribos release on PyPI to reflect the many updates since
  it was last released
- Exploring multithreading for performance/time improvement in test runs, to
  make them more viable for gate jobs or similar
- Enabling Syntribos to understand context beyond a single request (i.e. enable
  tests to create, then read, modify, and delete a resource)
- Rethinking request templates by using a less cluttered/repetitive format, and
  giving more information to Syntribos for improved testing accuracy
- Stretch goal: Adding more formatters for results output (e.g. HTML,
  human-readable text)
- Further improving test reliability & confidence, and reducing false positives


Members of Syntribos Team
==============================

- Aastha Dixit ([Github][Aastha_github]) - Intel
- Charles Neill ([Github][Charles_github]) - Rackspace
- Khanak Nangia ([Github][Khanak_github]) - Intel
- Matt Valdes([Github][Matt_github]) - Rackspace
- Michael Dong ([Github][MD_github]) - Rackspace
- Michael Xin ([Github][MX_github]) - Rackspace
- Rahul Nair ([Github][Rahul_github]) - Intel
- Vinay Potluri ([Github][Vinay_github]) - Intel


[1]: https://review.openstack.org/#/q/(owner:%22Rahul+U+Nair%22+OR+owner:%22Charles+Neill%22+OR+owner:%22Aastha+Dixit%22+OR+owner:%22Khanak+Nangia%22++OR+owner:%22Vinay+Potluri%22++OR+owner:%22Michael+Dong%22)+-project:openstack/syntribos
[2]: https://review.openstack.org/#/q/(reviewer:%22Rahul+U+Nair%22+OR+reviewer:%22Charles+Neill%22+OR+reviewer:%22Aastha+Dixit%22+OR+reviewer:%22Khanak+Nangia%22++OR+reviewer:%22Vinay+Potluri%22++OR+reviewer:%22Michael+Dong%22)+-project:openstack/syntribos
[3]: http://stackalytics.com/?release=newton&project_type=openstack&module=syntribos
[4]: https://github.com/openstack/syntribos/tree/master/examples/templates

[syntribos]: https://github.com/openstack/syntribos
[OSIC]: https://osic.org/
[keystone]: https://github.com/openstack/keystone
[neutron]: https://github.com/openstack/neutron
[glance]: https://github.com/openstack/glance
[nova]: https://github.com/openstack/nova
[cinder]: https://github.com/openstack/cinder
[swift]: https://github.com/openstack/swift

[Aastha_github]: https://github.com/aasthadixit
[Charles_github]: https://github.com/cneill
[Khanak_github]: https://github.com/knangia
[Matt_github]: https://github.com/mattvaldes
[MD_github]: https://github.com/MCDong
[MX_github]: https://github.com/jqxin2006
[Rahul_github]: https://github.com/rahulunair/
[Vinay_github]: https://github.com/vinaypotluri
