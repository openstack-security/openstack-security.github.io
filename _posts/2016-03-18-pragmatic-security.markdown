---
layout: post
title:  "Pragmatic Security: When Your PoC Goes into Production"
date:   2016-03-18
categories: security
tags: security openstack
author: "sicarie @ Hewlett Packard Enterprise"
---

![Pragmatic Security: When your PoC Goes into Production](http://s22.postimg.org/mruu1gim9/cloud_computing_button_blue.jpg)

## Creating a Cloud Security Program

A common anecdote when looking at OpenStack cloud deployments is that when
an issue arises - such as with timetables or migrating an application to a
cloud-native architecture - that security in one of the first items to slip
from the schedule. So when your Proof-of-Concept cloud is ready to be
deployed in Production, there are occasional gaps in the overall security
and assurance of the environment.

As every environment is different, this will be a "one size fits all" post,
and it is up to the reader to adapt the recommended Security Software
Lifcycle Management program to their environment.


## Teams

Teams will be referenced in these posts with as much clarity as possible,
and our assumption is that they are roughly assigned as service teams -
which would take care of an individual OpenStack service such as Nova -
and development teams - that are in charge of the applications that run
on the deployment. In your situation, this may be able to be directly mapped
to individual teams, a single team, individuals responsible for a given service,
or even a single individual. It will be up to you to determine what team is
best to engage for a given issue.

Each team should be responsible to a master architect - a single technical
resource that is tasked with overseeing the integration details for each
service and application to ensure they are all able to integrate and develop
together for future integrations.

Additionally, there should be a dedicated security architect who will work with
both the service teams, development teams, and master architect to ensure the
security of the OpenStack deployment. The Security architect should not be
responsible to the master architect, but rather a peer that is able to
influence priority and build features.


## The Gate

It is also assumed that you are utilizing some type of version-tracking software
such as git or SVN. Both your services, configurations, orchestration, and
application teams are utilizing these version-tracking applications for code
check-in and to then trigger gate and build jobs.

This article will assume that Git is used for versioning, and Jenkins for
check-in jobs like pep8.

The repositories that approved check-ins are merged into can be considered
the 'source of truth' for code and configuration information in a running
environment.


## Security Activities

The security team will work to build security and assurance through each step
of the software lifecycle. Traditionally, this is encompassed by host hardening,
code review, and firewall/network ACLs. In a cloud native environment, there are
a few additional recommended steps. Additionally, the Security Team will also
interpret and maintain the Security Policy.


![Secure Architecture](http://s27.postimg.org/3xtqknmdv/th_1.jpg)
## Secure Architecture

The Security team works with each service team to identify the best practice
approach for a given service, the threat landscape, and secure methods to any
identified threat vectors. These are captured in network diagrams, wiki pages,
and configuration management databases for reference by the teams required to
implement the devices.


## Threat Analysis

Once a secure architecture has been documented, the security team and major
stakeholders would be invited to a meeting that critically analyzes each service
in context where the security architect who influenced the architecture
introduces it to the rest of the security team and stakeholders to get addtional
points of view of exposure and possible exploit vectors for review.


## Static Analysis

On a per-application basis, the appropriate static code analysis tool can be
selected and included in the gate so that "low hanging fruit" can be identified
and fixed by a developer on check-in, and not depend on other developers or an
offical code review by an external party.


## Continuous Assurance

The virtual machines used to host the applications will also need to be hardened,
and can be through an orchestration tool such as Chef or Ansible. Once a secure
baseline has been determined, the orchestration tools can be used to deploy the
proper versions of packages and utilities and bring each host up into a known
hardened state.


![Regular Review](http://s12.postimg.org/t6vf6afft/image.jpg)
## Regular Review

Additionally, the policies, configurations, and results of the above should be
validated on a regular cadence. Scheduling regular reviews for each - such as
starting with an annual review of each, and then increasing as needed - will
ensure the controls are accurately applied for the current environment.
