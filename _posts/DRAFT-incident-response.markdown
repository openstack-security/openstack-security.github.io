
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
