---
layout: post
title:  "A Path across the Desert: Improving Security in Sahara"
date:   2016-02-25
categories: sahara
tags: sahara bandit barbican
author: "elmiko @ Red Hat, Inc."
---

![Caravan in the desert](http://i.imgur.com/9Nv302W.png)

Over the past few cycles I have had the pleasure of working with the
OpenStack Security Project (OSSP) on behalf of the Sahara team as our cross
project liaison. During this time I have learned a great deal,
witnessed the birth of a few awesome projects (Bandit, Anchor,
Syntribos, to name a few), and had the opportunity to use these
experiences to improve the internal security of Sahara.

In this post I'd like to describe some of the changes we have made to
improve security in Sahara, and how working with the OSSP has greatly
increased my awareness of, and answer to, many security issues in
OpenStack and in general.

# What is Sahara?

The [Sahara project](https://github.com/openstack/sahara) is the Data
Processing service for OpenStack. But, what does this mean exactly? It
means that Sahara provides a one-stop shop for launching, maintaining,
and operating many popular data processing frameworks and their
supporting infrastructures. Technologies such as;
[Hadoop](https://hadoop.apache.org), [Spark](https://spark.apache.org),
[Storm](https://storm.apache.org),
[Oozie](https://https://oozie.apache.org/),
and [ZooKeeper](https://zookeeper.apache.org/), as well as a host of
related applications can all be found in Sahara. These implementations
are not limited to the standard installs either, there is also support
for distributions from [Cloudera](https://www.cloudera.com/),
[Hortonworks](http://hortonworks.com/), and [MapR](https://www.mapr.com)
included.

If you are interested in enabling "Big Data" applications on your
OpenStack deployment, then let the Sahara project be your guide to
safely cross the desert to the rich oasis of data analytics.

# How have we improved Sahara?

Since the Icehouse release, the Sahara project has actively reached out
to the OSSP to learn more about the ways that we can better harden
it for production deployments. There are several key features which
have blossomed as a direct result of this relationship.

[Object Storage access using proxy users](http://docs.openstack.org/developer/sahara/userdoc/advanced.configuration.guide.html#object-storage-access-using-proxy-users)
is a feature that was implemented to help operators and users by
reducing the need for distributing a users' credentials to cluster
nodes. Traditionally, these credentials have been used to access the
OpenStack Object Storage service, the
[Swift project](https://github.com/openstack/swift), by applications
running within a Sahara cluster to store and retrieve data. This
feature obviates that need by using short term, ephemeral, users with
narrowly defined permissions to perform the access on behalf of the
user.

The addition of the
[Bandit project](https://github.com/openstack/bandit) to Sahara's
continuous integration gates has lead to the discovery of several bugs
and areas of improvement for the project. This tool has been a vital
step in our process of locating weak points within the codebase.

[Integration with the OpenStack Key Manager service](http://docs.openstack.org/developer/sahara/userdoc/advanced.configuration.guide.html#external-key-manager-usage)
is another effort which has been greatly aided by involvement with the
OSSP. Through engagement, we were able to learn a great deal about the
[Barbican](https://github.com/openstack/barbican) and
[Castellan](https://github.com/openstack/castellan) projects. This
experience lead to the integration of Sahara with Barbican through the
Castellan library. In so doing, the project has been able to migrate
its internal storage of sensitive data to the external key manager thus
maximizing the hardening of this information.

# Strength in numbers

I can't emphasize strongly enough how our participation with the OSSP
has helped the strength of the Sahara project. I feel that the
community which regularly attends the OSSP meetings, and the extended
community of developers, researchers, and operators who particpate with
the group have been a great resource for furthering our goal of
building better security.

![Whiteboard](http://i.imgur.com/44CyKaJ.jpg)

While attending the weekly meetings, mid-cycle sprints, and summit
sessions hosted by the OSSP, I have found a great spirit of comradery
and an openness to reach out for the purpose of sharing vital security
information. There have been in-depth discussions of theoretical
deployment strategies, hackathon sprints, and presentations on some of
the cutting edge software that is being developed by the OpenStack
community.

#Looking to the future

For the Sahara project, we will continue our participation with the
OSSP. I am excited by the work that is being done around API
[fuzz testing](https://en.wikipedia.org/wiki/Fuzz_testing) with
projects like [Syntribos](https://github.com/openstack/syntribos). I am
also curious to continue the discussion about methods for distributing
keys and other sensitive information to applications that exist within
the project network space (sometimes referred to as the overcloud).

The work continues on securing Sahara through feedback from Bandit, and
I am confident we will soon have a fully voting gate for the project.
We also have continued work to do with regards to improving Kerberos
integration with Hadoop based technologies.

If you work with an OpenStack project or community, and are interested
in improving security,  I hope I have at least inspired you to visit the
Security Project and investigate how we can join forces to improve
OpenStack.

