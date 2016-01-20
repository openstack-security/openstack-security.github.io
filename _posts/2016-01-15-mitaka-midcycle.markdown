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

## Barbican Overlap
This was the first Security mid-cycle where we had scheduled a
deliberate overlap with another OpenStack project. Having our mid-cycle
take place at the same time as the [Barbican](https://wiki.openstack.org/wiki/Barbican)
project makes a lot of sense; there are some clear synergies between our
groups and some shared objectives. Key topics included multiple HSM
backend support (not all secrets are created equal), BYOK (more on that
below) and the potential separation of the Certificate Management
Services (CMS) from the existing Key Management Services (KMS) within
Barbican.

## Barbican CMS Refactoring
The main driver for this being that CMS is secondary to KMS.
A CMS may well require a KMS to run but the reciprocal is not true. The
general conclusion after discussion was that it makes good engineering
sense to refactor away CMS. However, this is a significant body of work
and it is unclear when this might start. One option that was discussed
was for the Security Project to foster the CMS refactor/rebuild as we
already have several ([anchor](https://github.com/openstack/anchor),
[killick](https://github.com/openstack-security/killick)) PKI projects
in flight.  

## PKI, TLS and Ephemeral Things
A popular discussion topic was that of
[Anchor](https://github.com/openstack/anchor) and more general PKI
issues. Anchor (and systems like it) issue short-lived certificates to
services that require them - be they server side services or client
applications. The main advantage of short-lived certificates is that
they work around the common shortfalls of traditional revocation
techniques.

A certificate is in essence an attestation from a third party that a
server or client is who it claims to be. Any system that trusts the
third party will trust certificates provided by it. As certificates are
often granted for years, it is of the highest importance that a
certificate can be revoked if that trust is undermined - as in the case
of a compromised private key (_remember heartbleed?_) of similar loss of
integrity.

### Typical Revocation
Certificates are typically revoked through two means. The first are the
somewhat traditional Certificate Revocation Lists (CRL) - a signed list
of revoked certificate fingerprints. There are significant real world
problems with implementing CRLs today. Lets start with the obvious. Try
searching your hard drive for a CRL (_it's ok, I'll wait_) - couldn't
find any could you? That's because operating systems don't ship with
CRL files any more, over the years the CRL files of major internet
Certificate Authorities have grown to be several GB large and
subsequently aren't shipped with any major OS and are rarely downloaded
by any of the commonly installed crypto suites (the collection of
services and libraries that provide cryptographic functionality to
applications).

### Usage within OpenStack
Thankfully the indomitable [Major Hayden](https://major.io/)
of Rackspace has already written up a mailing list
[post](http://lists.openstack.org/pipermail/openstack-dev/2016-January/084213.html)
and an accompanying [etherpad](https://etherpad.openstack.org/p/openstack-ansible-tls-improvement)
discussing how TLS might be improved in [OpenStack Ansible](https://github.com/openstack/openstack-ansible).

## Threat Analysis Methodology
During the mid-cycle we worked to document at process for performing
threat analysis that can be utilized by developers. This is the subject
of it's own post [here](some-post-markup)

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

## Project Maturity Tags and Metrics

## BYOK
Bring your own key

## OpenStack Ansible Security

## Syntribos

# Slippage - those things we couldn't quite make fit
