---
layout: post
title:  "Ephemeral PKI"
date:   2016-01-20
categories: tooling
tags: Ephemeral PKI, Anchor
author: "hyakuhei @ Hewlett Packard Enterprise"
---

# PKI, TLS and Ephemeral Things
A popular discussion topic at the recent [mid-cycle]({% post_url 2016-01-15-mitaka-midcycle %})
was that of [Anchor](https://github.com/openstack/anchor) and more
general PKI issues. Anchor (and systems like it) issue short-lived
certificates to services that require them - be they server side
services or client applications. The main advantage of short-lived
certificates is that they work around the common shortfalls of
traditional revocation techniques.

A certificate is in essence an attestation from a third party that a
server or client is who it claims to be. Any system that trusts the
third party will trust certificates provided by it. As certificates are
often granted for years, it is of the highest importance that a
certificate can be revoked if that trust is undermined - as in the case
of a compromised private key (_remember heartbleed?_) of similar loss of
integrity.

![Screenshot of chrome failing certificate validation for mcafeestore.com](http://news.netcraft.com/wp-content/uploads/2013/05/mcafeestore-chrome-win-2.png)

## Typical Revocation
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

![Microsft CRL Information Window](http://blogs.technet.com/cfs-file.ashx/__key/communityserver-blogs-components-weblogfiles/00-00-00-89-67/3326.1.JPG)

In order to provide a scalable revocation mechanism for PKI,
[RFC 6960](https://tools.ietf.org/html/rfc6960) - "Online Certificate
Status Protocol" was drafted. This protocol is a lightweight live
verification system, where a service can verify a certificate in
realtime by querying an OCSP responder - a service operated by the
Certificate Authority that issued the certificate. This protocol is what
is generally used for certificate revocation by web browsers today.
However, there are a few problems when trying to use OCSP for local
networks, one of the biggest is that OCSP suffers from a replay attack.
An attacker can capture a legitimate 'Certificate OK' response and
play that back to a querying service that is being attacked, even after
a certificate has been revoked. Some methods exist to mitigate against
these attacks, including the option inclusion of an [nonce](https://en.wikipedia.org/wiki/Cryptographic_nonce)
however it should be noted that most cryptographic libraries don't
support the nonce and that even when they do, OCSP responses normally
have a 24 hour expiry window, which means the response can often be
replayed even if an nonce is in use. A recent [Mozilla article](https://wiki.mozilla.org/CA:ImprovingRevocation)
mentions that OCSP responders are [not yet reliable enough](http://news.netcraft.com/archives/2013/04/16/certificate-revocation-and-the-performance-of-ocsp.html)
 to allow browsers to hard-fail on missing OCSP responses. Meaning that
 attackers who control part of a network - _something PKI is supposed to
 help defend against_ - can render revocation useless by denying access
 to OCSP responders.

![Cat Meme "Tell me again... That revocation works"](http://i.imgur.com/bTyE2Qc.jpg)

On paper, PKI is very secure, in practice it's not always the most well
implemented of security mechanisms. Although this is a little off-topic
I'd suggest the reader checks out "More Tricks for Defeating SSL" - a
talk given by Mixe Marlinspike at Defcon 17 - it's just a great
presentation with excellent related content - skip to 35:20 for some
scary stuff around revocation - the attack doesn't work any more but it
is one of my all time favorite vulnerabilites

<iframe width="560" height="315" src="https://www.youtube.com/embed/5dhSN9aEljg" frameborder="0" allowfullscreen></iframe>

The biggest issue with OCSP with regard to OpenStack is that it's very
rarely implemented in the various cryptographic libraries available for
Linux.

## Passive Revocation
The OpenStack security team developed a PKI system for use inside
OpenStack that doesn't perform either form of traditional revocation.
The [Anchor project](https://github.com/openstack/anchor) uses a system
of 'Passive Revocation' - it issues very short lifetime certificates and
instead of revoking bad certificates it will instead simply refuse to
issue new ones for a client system that has been revoked.

![Anchor top level diagram](https://dl.dropboxusercontent.com/s/imz9t10bf54eesq/Screenshot%202016-01-20%2018.07.09.png)

This is obviously a big departure from more traditional certificate
issuance models and it brings with it some new requirements. The primary
one being that now machines that need to use certificates must request
certificates significantly more often, which necessitates an automated
certificate issuing capability. Anchor provides this service with robust
authentication and systems for understanding if a certificate meets
various policy constraints.

I've spoken at length on Anchor, so instead of repeating all of the
details here, I've embedded a couple of youtube links from summit talks:

<iframe width="560" height="315" src="https://www.youtube.com/embed/jf_YOzW7I3s" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Q_ZhrQq-_YM" frameborder="0" allowfullscreen></iframe>

## Usage within OpenStack
Anchor is best used to provide internal TLS within OpenStack
deployments. It's currently leveraged within the HPE Helion cloud
product and I'm glad to be able to write that after some discussion at
the [Security Mid-Cycle]({% post_url 2016-01-15-mitaka-midcycle %}) the
indomitable [Major Hayden](https://major.io/) of Rackspace has already
written up a mailing list [post](http://lists.openstack.org/pipermail/openstack-dev/2016-January/084213.html)
and an accompanying [etherpad](https://etherpad.openstack.org/p/openstack-ansible-tls-improvement)
discussing how TLS might be improved in [OpenStack Ansible](https://github.com/openstack/openstack-ansible).
