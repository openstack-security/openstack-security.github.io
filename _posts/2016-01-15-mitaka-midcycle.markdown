---
layout: post
title:  "Mitaka Mid-Cycle"
date:   2016-01-15
categories: mid-cycle
tags: mid-cycle collaboration mitaka rackspace
author: "hyakuhei @ Hewlett Packard Enterprise"
---
This post (and this blog) comes into being at the end of an extremely
busy week for the Security Project. Members of the team have gathered
at the [Rackspace](https://www.rackspace.com/) Castle (!?) in San
Antonio to discuss various OpenStack security issues, drive code sprints
on important project features and collaborate on new projects
(_spoiler: We're rebooting lightweight Threat Analysis_)

Our Rackspace hosts were gracious and accommodating. I'd like to
personally extend my thanks to them for hosting us and allowing us to
use the resources, meeting rooms and free coffee that Rackspace offers
to it's own Rackers.

Special thanks to [Michael Xin](https://twitter.com/securitycabinet)
for organizing the logistics for the mid-cycle - his diligence ensured
we had a well located, fed and watered security team!

# Mid-Cycle Rundown
In the leadup to the mid-cycle we created an [etherpad](https://etherpad.openstack.org/p/security-mitaka-midcycle)
to capture a number of the themes we wanted to cover during the week.
To kick the week off we held an [unconference](https://en.wikipedia.org/wiki/Unconference)
which resulted in a full (ambitious?) schedule for the week...

![Postit Note Schedule](https://drive.google.com/uc?export=download&id=1H_nwKFPTYAAAboKiMO5WitLAPxHbn2kmxQ)

In this inaugural blog post I'll try to provide a brief overview of some
of the topics we focussed on, what progress was made and what actions we
have committed to moving forward.

# Barbican Overlap
This was the first Security mid-cycle where we had scheduled a
deliberate overlap with another OpenStack project. Having our mid-cycle
take place at the same time as the [Barbican](https://wiki.openstack.org/wiki/Barbican)
project makes a lot of sense; there are some clear synergies between our
groups and some shared objectives. Key topics included multiple HSM
backend support (not all secrets are created equal), BYOK (more on that
below) and the potential separation of the Certificate Management
Services (CMS) from the existing Key Management Services (KMS) within
Barbican.

# Barbican CMS Refactoring
The main driver for this being that CMS is secondary to KMS.
A CMS may well require a KMS to run but the reciprocal is not true. The
general conclusion after discussion was that it makes good engineering
sense to refactor away CMS. However, this is a significant body of work
and it is unclear when this might start. One option that was discussed
was for the Security Project to foster the CMS refactor/rebuild as we
already have several ([anchor](https://github.com/openstack/anchor),
[killick](https://github.com/openstack-security/killick)) PKI projects
in flight.  

# PKI, TLS and Ephemeral Things
A popular discussion topic was that of
[Anchor](https://github.com/openstack/anchor) and more general PKI
issues. Anchor (and systems like it) issue short-lived certificates to
services that require them - be they server side services or client
applications. The main advantage of short-lived certificates is that
they work around the common shortfalls of traditional revocation
techniques.

![Cat Meme "Tell me again... That revocation works"](http://i.imgur.com/bTyE2Qc.jpg)

This topic is discussed in a lot more detail in the recent
[Ephemeral PKI]({% post_url 2016-01-20-ephemeral-pki %}) blog post.

# Threat Analysis Methodology
During the mid-cycle we worked to document at process for performing
threat analysis that can be utilized by developers. This is the subject
of it's own post [that you can read more about here]({% post_url 2016-01-16-threat-analysis %})

![Whiteboard Threat Analysis from the mid-cycle](https://drive.google.com/uc?export=download&id=1AFZsdYKx1cvlA6a78ynRv_t-dS1n9Qeygw)

Our aim is to create a methodology that:

* Identifies all entry points into the system
* Identifies all the assets that are at risk
* Identifies where data is persisted
* Documents how data travels between components of the system
* Documents data formats and transformations
* Documents external dependencies
* Establishes the threat actors that they system defends against (and those it does not).
* Documents the impact of degrading controls

The [etherpad](https://etherpad.openstack.org/p/security-mitaka-midcycle-threatanalysis) for threat analysis contains our current notes on this project.

# Project Maturity Tags and Metrics
Our goal is to work with the OpenStack Foundation to make security
quality part of the maturity metrics for a project, both by applying
security gate checks as well as by undertaking appropriate threat
analysis.

![Project Maturity Ratings](https://drive.google.com/uc?export=download&id=0B0osRPn3qBq5bVNXSWdZSWdDeTA)

While the security project creates infrastructure tools like [Anchor](https://github.com/openstack/anchor)
it also creates security enhancement tooling like [bandit](https://github.com/openstack/bandit)
for static code analysis and [syntribos](https://github.com/openstack/syntribos)
for API fuzzing. Of the two Bandit is a little more mature and is
already incorporated into the CI gates of security related projects such
as Keystone and Barbican.

A new project we are working on, discussed above and in more detail
[here]({% post_url 2016-01-16-threat-analysis %}) is Threat Analysis.
Our intention is to quickly mature this project by iterating on security
enhancing projects: Anchor, Barbican, Keystone etc.

Eventually we'd like the application of all these projects to be
incorporated into the [maturity](https://www.openstack.org/software/project-navigator/)
of a project. Security is one of the primary [blockers](http://www.out-law.com/en/articles/2015/june/cloud-adoption-hindered-by-concerns-about-security-privacy-and-lack-of-control-survey-finds/)
to cloud adoption. I personally think it's a little scary that
OpenStack has come so far without more formal security verification and
documentation.

# Bring Your Own Key
This was a combined discussion between the Barbican development team and
members of the security project. Encryption is coming to OpenStack -
Barbican provides vital Key Management Services (KMS) for OpenStack
projects to manage keys for cryptographic operations. Nova, Cinder and
Swift are all expected to have encryption capabilities in the next 1-2
release cycles.

Our discussion focussed on what a "Bring your own key" model might look
like for OpenStack. This seems to be a big gap for OpenStack today as
it is a feature that is already implemented by [AWS](https://aws.amazon.com/blogs/aws/s3-encryption-with-your-keys/)
, [Google](http://googlecloudplatform.blogspot.co.uk/2015/07/Bring-Your-Own-Encryption-Keys-to-Google-Cloud-Platform.html)
and [Azure](https://technet.microsoft.com/en-gb/library/dn592126.aspx)

![Discussing Swift Encryption Workflow](https://drive.google.com/uc?export=download&id=0B0osRPn3qBq5dXVubHJGLUJiR0E)

This is going to become a new activity for the security project and will
fall into two quite separate tasks (that may be run in parallel). The
first is to discuss what a key extension to the APIs of each of the IaaS
services offering encryption would look like. The expectation is that
we could add the same API extension to each service, likely an HTTP
header that describes a key to be used for an operation. The second task
is to understand how the key material will be used by each service. The
expectation is that this should be easy for services that are using
[Castellan](https://github.com/openstack/castellan) as hopefully the
key header can just be passed along to the Castellan middleware which
would use the provided key rather than sending a request to Barbican.

As with all things crypto, the devil is in the detail, we hope to
raise this as a cross-project topic at the next OpenStack summit in
[Austin](https://www.openstack.org/summit/austin-2016/)

# Other Topics
Lots of other things were covered at the mid-cycle that I haven't
documented here:

* Syntribos - API fuzzing (A post on that is coming soon)
* Bandit 1.0 level settings
* Anchor 1.0 stabilization and CMC additions
* OpenStack Ansible Security demonstration

... and of course the important discussions that people have that just
would not take place without everyone being in the same room :)

# Slippage - those things we couldn't quite make fit

* A sprint on [OpenStack Security Notes](https://wiki.openstack.org/wiki/Security_Notes)
* Improvements to the [Security Guide](http://docs.openstack.org/sec/)
