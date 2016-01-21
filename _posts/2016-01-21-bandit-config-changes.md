---
layout: post
title:  "Bandit Config Changes"
date:   2016-01-21
categories: bandit
tags: bandit
author: "tmcpeak @ Hewlett Packard Enterprise"
---
## The problem - current Bandit config is... not great
One of the most consistent pieces of feedback we've gotten is that Bandit's
config files are unwieldy and painful to use.  Config files in Bandit have
traditionally been used for a few unrelated things, but the most common use
was for a project to specify which tests they want to run.

If a project wants to start using Bandit today they typically create a copy
of the config file, define a profile within the config file that lists which
tests should be included, and then run Bandit with that profile.  There are a
few problems with this approach though.  There really haven't been any good
ways to find out what all of the plugin options are.  So it's harder than it
should have to be for a project that adopted Bandit several versions ago to
find out what new plugins are available.  Listing out plugins by name in the
config file is also tedious and error prone.

![Rage](https://openstack-security.github.io/assets/rageguy.jpg)

Config files have also traditionally contained all of the settings for each
plugin.  The idea was that projects may want to tune plugins in certain ways,
but in practice we've found most don't.  They'd far rather have sane defaults
with the ability to change a few values if required.

These and other frustrations with the current Bandit config have led us to
rethink Bandit configs entirely and we believe we've come up with something
that we believe will make it far easier to use.

## The solution - get rid of config for most users
We're doing a few things to remove the need for config.  All plugins will have
a canonical ID (ie: B101).  Projects that want to run (or exclude) specific
plugins can pass these on the command line.  So you can run something like:

`bandit -i B101,B102,B103`

If you find yourself using a specific set of tests you can also list these
out in a separate profile file, which can include or exclude tests by name
or ID.  We believe profile files will be useful for workflows like penetration
testing, where you want to run the same set of tests and don't want to have
to copy-paste commands.

![Happy](https://openstack-security.github.io/assets/happyguy.jpg)

What about settings?  Settings are now built into the plugins themselves.
We'll have commands that expose the configurable settings, but most users
will probably just want to use the default.  If you do want to override a
particular setting you can just put the one or two you want to change in
your profile.

## What about projects that already use Bandit?
For OpenStack projects that have been using config, we'll propose the
appropriate changes for you when the config changes are ready - you won't
have to do anything.  For other users that want help porting their config
files over, please reach out to us - we're happy to help!

## Feedback welcome!
If you have any thoughts or questions about the config change please come
to one of our weekly Security IRC meetings or drop by on #openstack-security.
