---
layout: post
title:  "An Overview of Incident Response with OpenStack Clouds"
date:   2016-03-18
categories: security
tags: security openstack incident-response
author: "sicarie @ Hewlett Packard Enterprise"
---

! [OpenStack Incident Response]()

## Initial ideas

Incident response in the cloud is the same as incident response in real life, the only
differences are that they're different.

Same: identify, isolate, triage
Different: identify, isolate, duplicate, triage

Same: Identify a possibly compromised host
Different: Identify a possibly compromised host at scale

Same: Isolate
Different: vlan it off, or just kill it (after copying of course)

Same: Triage & analyze how
Different: vm image, image copy (be careful, some images will be deleted by a copy) to secure storage, mount virtual image; more consistent layout (especially if using orchestration)

Different: on isolate, it's cattle so you can just duplicate another of the same type (if load requires)


# Alt outline


## Cloud IR Challenges

1. Identifying systems (floating IPs) & concerns
  * helps to be able to packet captures on physical and virtual network devices
  * and have ips to help auto-detect "low hanging fruit' attack traffic
2. Policy
  * do you take down the host and then investigate?
  * Do you wait for confirmation of malicious traffic (and possibly allow an attack in progress to continue or propagate) before isolating & traiging?
3. Legal, SLA and contractual agreements
  * Do you have agreements that dictate how a confirmed incident is handled (ie, uptime, data access, engagement, etc...)
  * Is this cloud in a single country? What are the regulations around data privacy?
4. Type of incident
  * DMCA vs ddos vs scan/attack traffic vs
5. necessary information capture
  * based on the image type, copying an image may cause deletion
  * capturing memory?
  * associating network traffic with instance
6. Prevelancy of vulnerability
  * how was the system compromised & does this attack vector exist across multiple systems? Or is this a "one-off" system?

Response:
Determine exploit path & associated users/creds
Revoke privileged access & outstanding sessions
Invalidate credentials (provision new auth & push to systems; or if systems are sensitive enough, disalble the user)

Review:
keystone token cache
new users
new roles (delegated tokens)

Then:
If it's not dmca/similar, identify if vuln is prevalent throughout fleet, and edge control or orchestration update to remediate
