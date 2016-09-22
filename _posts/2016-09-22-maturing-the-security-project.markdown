---
layout: post
title:  "Maturing the Security Project"
date:   2016-09-22
categories: Organization
tags: maturity PTL OSSP
author: "hyakuhei @ IBM Cloud"
---

This blog article is intended to address the recent discussions on the openstack-dev mailing list, following the suggestion by Thierry on behalf of the TC that the OpenStack Security Project "should be removed from the Big Tent" because the security team failed to nominate and elect a project ream lead (PTL) for the next release cycle. This process is required for all active project teams and is seen by the TC as a failure in community engagement that the OSSP has missed this deadline, again.

Back in the early days of the Security Project being in the big tent I missed the election deadline for my nomination. Pure oversight on my part, I was new to the role of PTL having been grandfathered in from the working group and I simply didn't realise what was required for elections. 'Missing a nomination once is bad, so missing the most recent nomination window is obviously very bad and raises questions over the level of engagement we have in the community, particularly as everyone in the OSSP also missed the email sent to highlight the closing nomination window (Its the one on the 19th)...

![PTL election reminder](../assets/SecurityMail.png)

Unfortunately during the nomination window I was temporarily distracted dealing with
some local issues. I've discussed these with a member of the TC who recognises that
it was a temporary thing that's unlikely to happen in the future, however the bell
has been rung and we must decide how to proceed.

## Maturing the Security Project
Missing two nominations reflects badly on a project team and leads to several understandable
[questions](http://lists.openstack.org/pipermail/openstack-dev/2016-September/104170.html) being
asked: _Who are these people?_ _Are they an active team?_ _Should they be moved outside of the big
tent?_

These are understandable questions, I feel that my [on-thread
response](http://lists.openstack.org/pipermail/openstack-dev/2016-September/104176.html) addressed
them for the most part. What I want to focus on is the things that we need to do to be a better part of
the community and ensure that project teams and the TC are both aware of what we do and how we help
improve security in OpenStack.

We know from the feedback we've had from downstream OpenStack consumers that our work
is valued, we need to better demonstrate that value within the OpenStack community. I think a good
place to start is to look at the [Project Team Guide](http://docs.openstack.org/project-team-guide)
examine what we are already doing and where we fall short. Of course this doesn't include the good
things we do like providing CI tooling for security, threat analysis etc but it is the minimum boxes
that we should be ticking off as a project team and that I should be driving as PTL.

I want to be clear, I think that the Security Project is doing great things to enhance security
in OpenStack. We need to become a better community player though, through doing so I expect
new opportunities to innovate on security and create new ways to make OpenStack more secure.

## Score Card
I'm proposing a score card for the security project, to ensure we're doing all that
we should be doing and identify those areas where we need to improve. I've based this
on the [Project Team Guide](http://docs.openstack.org/project-team-guide)

Requirement | Status | Notes |
------------|--------|-------|
Open Code | Achieved | All code in git and licensed appropriately
Open Design | Achieved | All design is open to the public, conducted at summits etc
Open Development | Achieved | We follow standard OpenStack best practice
Open Community | Needs Improvement | We have a gap around the mailing lists that we need to address
Public Meetings on IRC | Achieved | 1700UTC Thursdays #openstack-meeting-alt
Project IRC channel | Achieved | #openstack-security
Community Support Channels | Mostly Achieved | We are strong on Launchpad and IRC which is where 90% of our workload comes from however we need to pay more attention to the ML and ask.openstack.org
Planet OpenStack | Achieved | This security blog posts to planet openstack
Participate in Design Summits | Achieved | Regular, very well attended sessions
Release Management | Achieved | We have a number of software projects that we created to support or enhance security in OpenStack. As they're not directly consumed by OpenStack Operators they've not been part of the normal release cycle. Instead we follow the Independent release model.
Support Phases | Needs Improvement | Traditionally we have not followed the normal support phases for our projects because they have not been directly consumed by downstream OpenStack users. However there's a clear opportunity to get more in line with the rest of the OpenStack community here. This should make things like rolling Bandit changes out through CI easier.
Testing | Achieved++ | All of our software and documentation efforts have appropriate gate tests in place. Functional and Unit tests are in place where appropriate. We've also built tooling that other teams are using in their projects for Security gate tests. We're not just testing, we're also testing our integration with the projects that have adopted us.
Vulnerability Management | Achieved | Our software projects don't have the vulnerability managed tag, however as the OSSP we do triage any security issues in our own software following standard processes, this is best demonstrated with the recent XSS issue in Bandit https://bugs.launchpad.net/bandit/+bug/1612988
Documentation | Achieved | We have a lot of documentation out there for customers and consumers of openstack [OSSNs](https://wiki.openstack.org/wiki/Security_Notes), [security.openstack.org](https://security.openstack.org), the [security guide](http://docs.openstack.org/sec/) as well as developer documentation such as that for [Anchor](http://docs.openstack.org/developer/anchor/) and [Bandit](http://docs.openstack.org/developer/bandit/)

## The Four Opens
To paraphrase from the OpenStack [documentation](http://governance.openstack.org/reference/opens.html) it's
important that any project participating in the big tent adopt and practice
the "four opens". Open Source, Open Design, Open Development and Open Community.

For the most part we have done a good job of following these, all of our code is
developed under the appropriate Apache Licenses and all of our documentation efforts
like the security guide, security notes, threat analysis etc are all conducted
openly and use the same peer review tools as our code projects. We develop new
ideas in the open, attend design summits and encourage new contributions.

Where we have not done such a good job is with the Open Community goal. Of course
our team is open to new ideas and new contributions but we have not been as big
of a participant in the larger community as we could have been. Our work with the VMT
typically means that teams are driven _toward us_ when they require our assistance.

I'd like to expand a little bit more on what Open Community means and where we can improve. OpenStack
has some very good [documentation](http://docs.openstack.org/project-team-guide/open-community.html)
on this topic but again I'll paraphrase here.

**Public Meetings on IRC:** This is something that the security project has always
done. We can be found on #openstack-meeting-alt at 1700UTC every Thursday. Our
meetings are public and
[logged](http://eavesdrop.openstack.org/meetings/security/2016/) we have a standing
public [agenda](https://etherpad.openstack.org/p/security-agenda) that any developer
is welcome to contribute to if they want to participate in the meeting, we also welcome people dropping
by with questions, comments etc.

**Mailing Lists:** When the Security Project first formed we were a working group,
we had a separate mailing list that didn't get used for many things but for legacy reasons that I
can't remember (we've been doing security for OpenStack since Essex) we had a private list. As I said
it didn't get used much in our day-to-day and I think that's a bad practice that we carried across to
our big tent operations.

Largely I think this disconnect from the mailing list has arisen because it was not our experience
that we needed to use it. Most of our work has always come from teams reaching out directly to us,
typically via IRC. I think it will always be the case that teams will be more active on one
communication medium than another but I fully accept that to meet our obligations under the four
opens we must find a way to work more effectively on the mailing lists.

**Community Support Channels:** We manage all of our bugs on LaunchPad, that's the primary way we
interact with the VMT. Our IRC channel is reasonably active but as we've described above we certainly
need to do better on the mailing lists.

## Impact of removing Security from the big-tent
Although I think it's been addressed a number of times on the mailing-list
[thread](http://lists.openstack.org/pipermail/openstack-dev/2016-September/104176.html) I'd like to
reiterate two themes from the responses regarding concerns of removing Security from the OpenStack
big-tent.

**Legitimacy:** As can be gleaned from this blog, we haven't done the best job in making the wider
OpenStack community aware of what it is that we do, probably even some teams who are running Bandit
in their gate might not realise that it's a tool that we created for OpenStack to be more secure.
However even with teams that haven't heard of us, we are able to quickly gain traction when they see
that we are a 'proper' OpenStack project - the truth of the matter is that how most people see
OpenStack, you're either in the tent or you're largely an irrelevance. We know this because we started
outside of the tent and found it much harder to engage with teams where we could see there were
obvious security issues. Being outside of the big-tent will make it very difficult for us to act as an
authority for signing off that a project has taken reasonable security steps before applying for a
vulnerability managed tag, a relatively recent [change](https://review.openstack.org/#/c/294212/)

**Investment:** Running any OpenStack project requires investment, very few projects succeed based
only on people working on them in their spare time. For the most part investment here means giving
people time to contribute to Security as part of their working week, to provide funding for spaces
for meetings and mid-cycles and to cover the time and expenses of contributors travelling to design
summits etc. It's no secret from looking around OpenStack that some historically big contributors have
been scaling back the number of people they send to summits, the numbers of active contributor they
maintain etc. Having been in the position of lobbying various corporations for support in these areas
I cannot imagine a scenario where we could leave the big tent and continue to dedicate time to the
efforts we have in place.

Without the legitimacy we have from being part of the big-tent we will not get the investment
required to deliver and enhance security within OpenStack.

## Moving Forward
I think it's clear by now that **I want the Security Project to have the opportunity to
stay within the big-tent**. I'd like to **continue on as PTL** at least through a period of maturing
the Security Project to ensure that our baseline operations are aligned with what the wider community
expects of any big-tent project.

I want the opportunity to improve the score card above and have us achieving everything on that list.
I see no reason why we can't begin acting on these things now and that our status can easily be judged
on this basis during the next election cycle.
