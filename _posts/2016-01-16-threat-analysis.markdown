---
layout: post
title:  "Threat Analysis"
date:   2016-01-16
categories: collaboration
tags: mid-cycle collaboration mitaka threat analysis
author: "hyakuhei @ Hewlett Packard Enterprise"
---
Threat analysis is hard. At [Hewlett Packard Enterprise](http://www8.hp.com/us/en/cloud/helion-portfolio.html#!&pd1=2&pd3=2&pd5=2)
we have a small team of people dedicated to generating architecture
documentation and leading threat analysis sessions. We conduct threat
analysis in two phases. The first phase is to create architecture
documentation that reflects how a service operates and how it will be
deployed. This first phase is normally conducted by a dedicated security
architect, working closely with a subject matter expert from the product
or service that is under analysis.

Only a few OpenStack contributing organizations have formalized threat
analysis processes and generally speaking they are unwilling to share
this content publicly. Luckily both [Rackspace](https://www.rackspace.com/cloud)
and [Hewlett Packard Enterprise](http://www8.hp.com/us/en/cloud/helion-portfolio.html#!&pd1=2&pd3=2&pd5=2)
are prepared to contribute both expertise and existing architecture
diagrams to the OpenStack Security Project.

David Graves took an old high level threat analysis diagram from the HP
archives and annotated it (red text) to help explain a number of the
properties that go into a simple TA diagram.

![Nova threat analysis diagram](https://review.openstack.org/cat/220712%2C3%2Csecurity-threat-analysis/source/figures/Template_Architecture-diagram.png%5E0)

The second phase of threat analysis is to bring together security
experts, architects and reviewers as well as subject matter experts to
review the architecture and ask probing questions about configurations,
interfaces etc with the aim of finding vulnerabilities in the system
and documenting security best practice.

At HPE we aim to conduct analysis sessions in 2-3 hours but it's not
uncommon for reviews to take much longer and this time does
not include the work taken to generate the architecture documentation,
which is often several days of effort.

During the mid-cycle we worked to document a lightweight methodology for
threat analysis. The objective is to create a methodology that would
allow project teams to document their own reference architecture during
one-two mid-cycle working sessions. We do not expect that this
methodology will be as complete as those mutli-day efforts that HPE and
Rackspace undertake but it will serve several important purposes. It
will define a standard for documenting reference architectures for
OpenStack projects and provide a solid base for future, iterative work
on threat analysis.

![Whiteboard Threat Analysis from the mid-cycle](https://drive.google.com/uc?export=download&id=1AFZsdYKx1cvlA6a78ynRv_t-dS1n9Qeygw)

There will of course be significant followup work from this week's
efforts and I'm glad to share that we have commitment from Redhat, IBM,
HPE, Rackspace and others.

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
