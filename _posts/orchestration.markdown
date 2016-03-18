Cloud means dynamic threat response
Hardening with orchestration
Orchestration vs 'golden image'

No intro to orchestration, no intro to server hardening; you get to google those

build a small base profile w/simple hardening bits
   - fail2ban
   - users & ssh keys
   - hostname matches standard
   - root user / ssh / localmail hardening
   - logging is configured properly

extend profile through system types (db/compute/network/etc...), or through data classification (x servers are more sensitive and get #allthesecurity)
   - selinux or apparmor profile is applied to the right server type
   - validate specific languages are (or are not) installed

This can also allow you to ensure that when a system comes up, it can have specific package, versions, and libraries installed (patching)

be aware of orch-tool specific security
   - ansible is ssh, so user/key mgmt, etc...
   - chef?
   - salt?
   - heat user is cloud admin, may want to disable after install
