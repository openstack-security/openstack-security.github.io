
So you have this PoC OpenStack cloud that has been proved, application migrated,
and deployed into Production. Now that the configs have been migrated, and you
have organized your team to be effective per the last post. Now you're looking
to ensure that the vulnerability surface of this shiny new toy is as small as
possible.

This article will walk through preapring for and setting up the Bandit static
code analysis tool for Python applications in the gate, which will allow
automated capture of "low-hanging-fruit" of security issues before they are
merged into the code base. This article assumes that code is again, in a Git
repository, and that Jenkins is used for build jobs.

The first step to doing this is to run Bandit on your project. This will give
you an idea of both the expected issues the first time Bandit is introduced into
the gate, as well as an initial report to begin remediation. The other
advantage is that you can provide a report of issues to the application team
prior to having it run in the gate so that significant issues can be handled
before check-in.

Additionally, the submission of this inital report can also link to the OpenStack
Developer Guidance methodologies that can be used as a reference for secure
coding.

https://github.com/openstack-security/Developer-Guidance
https://wiki.openstack.org/wiki/Security/Projects/Bandit#Gate_Testing_with_Bandit
https://wiki.openstack.org/wiki/Security/Projects/Bandit#Gate_Testing_with_Bandit
https://review.openstack.org/#/c/286892/
https://review.openstack.org/#/c/286912/
