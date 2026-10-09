# Assignment 1 — Failure Path Register

| ID | Failure point | Designed response | BPMN technique |
|:--:|:--|:--|:--|
| F1 | Missing fields or invalid team data | Return a targeted correction request; limit correction to two attempts | XOR + bounded loop |
| F2 | Team violates membership or size rules | Notify the team and close invalid submission | Business rule + error end |
| F3 | Duplicate / plagiarised topic | Review match and request new topic or record rejection | Service task + XOR |
| F4 | Submission deadline passed | Request late approval; close if declined | Interrupting timer + XOR |
| F5 | Committee asks for revision | Return proposal to team and revalidate on resubmission | Revision loop |
| F6 | Committee rejects | Send reasons and close proposal | Send/service task + end event |
| F7 | Committee review misses SLA | Send reminder and escalate to HoD without cancelling review | Non-interrupting timer boundary |
| F8 | No suitable guide available | Coordinator appoints manual/co-guide allocation | Business rule + user task |
| F9 | Guide is silent | Exclude guide and rerun matching | Timer boundary + loop |
| F10 | Allocation notification fails | Retry and fall back to coordinator notification | Error boundary + manual task |
| F11 | Withdrawal after allocation | Release guide slot and return team to allocation | Message boundary + compensation (documented control) |
