---
layout: post
title:  "Intrusion Detection"
date:   2016-05-16
categories: collaboration
tags: Intrusion Detection
author: "dlambrig@redhat.com"
---

A Network Intrusion Detection System (IDS) can watch traffic and warn an administrator when an attack or suspicious behavior occurs. This blog post will show how an IDS can be set up in OpenStack using one model and list architectural problems.

Call the *monitor* the OpenStack instance that runs the IDS. There are different locations where the monitor could be placed.

* The IDS can be placed between the instance and the network (as is the case for a firewall). In this case all traffic is inspected by the IDS before being forwarded to the destination.
* Traffic could be mirrored to the ID. In this case one copy of the traffic will reach the destination, and a second to the IDS.

Running an IDS in-band can impact performance. Therefore, this blog describes the second “mirroring” approach. The disadvantage is the threat will not be known until after the fact. This is a tradeoff that is often taken when using an IDS.

[Using mirroring with OpenStack](../assets/IDS-mirror-setup.png)

Call the IDS *administrator* the person who manages the monitor. It could be
* the tenant administrator
* the operator of the openstack cloud

The operator has full access to the cloud’s internal network. The tenant administrator only has access to required functionality needed to set up the IDS.

Certain networking functionality is needed to connect instances to be monitored to the IDS. One way to do this is with tap-as-a-service (TaaS). TaaS can be accessed via neutron commands. It is written using a plug-in architecture, and could have an interface from horizon. At the time of this writing such an interface has not been implemented. Only the operator has access to neutron commands, so TaaS is probably not an option (yet) for the tenant administrator.

Another option is Fuel contrail plug-in. That does have a GUI-based interface available to the tenant. This is available from Mirantis’ OpenStack distribution.

The tap is attached to the integration bridge.

[The OpenStack SDN](https://github.com/openstack-security/assets/IDS-sdn.png)

For more information in TaaS and Fuel contrail, including demos, see [1] [2] [3].

To set up OpenStack with TaaS using devstack, you can add the following lines to local.conf:

```enable_plugin tap-as-a-service https://github.com/openstack/tap-as-a-service
enable_service taas
enable_service taas_openvswitch_agent
```

In TaaS, a *flow* is a channel of traffic between a monitored instance and a monitor. A *service* is the monitor, in this case the IDS.

First create the service.

Then create a flow between each instance and the service.

You may see a small performance hit when you mirror data. It has been measured that mirroring can incur a performance hit.

In addition, it is probably better to run the IDS on a different node than the instances being monitored. Otherwise the IDS will take CPU cycles from other instances while processing mirrored traffic.

Once an attack is detected, the administrator can be alerted. The administrator may desire to take an action taken to block the attack - this is sometimes called an “automated response”. Such actions could add firewall rules, delete instances, or otherwise forcibly stop the threat.

A future blog post will explore running an IDS in containers. This configuration would scale elastically according to I/O needs. Other areas to explore are extraction of files from the network stream to run malware scans.

[1]

OpenStack Austin 2016 talk[link](https://www.openstack.org/videos/video/using-open-source-security-architecture-to-defend-against-targeted-attacks)

[2]

Devconf 2016 Intrusion Detection in the Cloud [link](https://www.youtube.com/watch?v=TT4ZBlAvo6M)

[3]

OpenStack Vancouver 2015 Tasp-as-a-Service [link](https://www.openstack.org/summit/vancouver-2015/summit-videos/presentation/tap-as-a-service-taas-port-monitoring-for-neutron-networks)

