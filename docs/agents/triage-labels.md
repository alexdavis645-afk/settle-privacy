# Triage Labels

Written by `factory adopt` from software-factory's label standard (`src/label-standard.mjs`), which every
owner repo follows. Change the standard, not this file.

Pick exactly one state for a new ticket: the first that fits of `needs-triage`, `needs-info`,
`ready-for-human`, `ct200-session`, `host-step`, `supervised`, `ready-for-agent`. `ready-for-agent`,
`supervised` and `host-step` are for factory projects only; a supervised ticket is not held for the owner.

The skills speak in terms of five canonical triage roles; each is the label of the same name here. When a
skill mentions a role (e.g. "apply the AFK-ready triage label"), use that label.

## State: exactly one on every open issue, except an `epic` or `retro`, which needs none

| Label | Meaning |
| ----- | ------- |
| `needs-triage` | Not yet sorted; the default for a new issue |
| `needs-info` | Waiting on the reporter |
| `ready-for-agent` | Factory projects only: specified and sandbox-checkable; built unattended, merges on the merge gate |
| `supervised` | Factory projects only: built in the sandbox once a person starts it, never by the batch; merge-gated |
| `host-step` | Only on projects that declare a host step: the build ends in it; a person starts it with factory run |
| `ct200-session` | Agent hand-work in an attended CT 200 session, including code on repos the factory does not build |
| `ready-for-human` | A person must act; with no human kind, the HITL desk can do it |
| `wontfix` | Will not be actioned; closed issues only |

## Human kind: only beside `ready-for-human`

| Label | Meaning |
| ----- | ------- |
| `needs-device` | Needs a device the desk lacks: iOS, watch, Pendant/BLE, real mic audio, outdoors, fingerprint |
| `alex-decide` | Waits on the owner's decision or ruling |
| `alex-grill` | The owner is grilled on it before it can be specified |
| `alex-external` | Needs the owner to act outside the repo |

## Shape and markers

| Label | Meaning |
| ----- | ------- |
| `epic` | Parent of sub-issues; never built itself |
| `spike` | Investigation that answers a question; nothing is built from it |
| `deferred` | Parked for later; sits beside the state the ticket returns to |
| `review-findings` | Findings from a review; carries needs-triage until triaged |
| `desk-triaged` | Triaged by the HITL desk |
| `founder-answered` | The owner has answered the questions in it |
| `recurring` | A retro whose cause was seen on three different days; read it first |
| `retro` | Filed by the factory about a run; closes itself when its source ticket merges or closes |

A `ready-for-human` issue with no human kind is one the HITL desk can do.

## `ct200-session` and the factory's own builds

`ct200-session`: agent hand-work in an attended CT 200 session: hosts, guests, live Home Assistant, credentials
or secrets, production or app-store writes, phone or iOS builds, live reads, and hand-built code on a repo the
factory does not build. Each state change still needs the owner's go-ahead. The factory never builds it and the
desk never claims it: selection never picks it, `factory run <project> <N>` refuses it, and `factory hitl queue`
lists it as kind `owner`, beside `supervised` and `host-step`.

A builder that stops because it needs a credential, or a host on a project without a host step, hands its
ticket to `ct200-session`, which then carries an executor kind: the credential or host it asked for. A host ask
on a project that declares a host step goes to `host-step` instead. Once the need is met, relabel the ticket
`supervised` or `ready-for-agent` to send it back to the factory.

| | `ct200-session` | `supervised` / `host-step` |
| --- | --- | --- |
| Who does the work | An agent in a CT 200 session, with the owner's go-ahead for each state change | The factory, in the sandbox, once a person starts it |
| Output | Changes on hosts, guests or CT 200 (recorded in the host map), or hand-built code | A pull request |
| How it ends | The session verifies it on the real system and closes it | Gate, review and the adversarial merge gate, then merge, unless it was started run-and-hold, it touches owner paths or the adversary says "your decision" |

## Exclusions

1. The eight states exclude each other.
2. `epic` and `retro` carry no state and exclude each other.
3. A human kind only sits beside `ready-for-human`.
4. `ready-for-agent`, `supervised` and `host-step` appear only on factory projects, and `host-step` only where the project declares a host step.
5. Work the factory can't build never carries a factory state: session work is `ct200-session`, person work is `ready-for-human`.
6. `spike` never sits beside a factory state.
7. `recurring` only sits beside `retro`.
8. `wontfix` allows only topic labels beside it.

Topic labels (`bug`, `enhancement`, `project:*` and the like) are this repo's own. The wayfinder skill's
`wayfinder:*` labels stay, always beside a state label.

## Merged labels

| Label | Becomes |
| ----- | ------- |
| `alex-supervised` | `supervised` |
| `alex-verify` | `ready-for-human` + `needs-device` |
| `design-ruling` | `ready-for-human` + `alex-decide` |
| `copy-ruling` | `ready-for-human` + `alex-decide` |
| `ralph-soon` | `deferred` |
| `paused` | `deferred` |
| `alex-other` | `ready-for-human` |
| `root-session` | `ct200-session` |
| `alex-grill` | keeps its label and gains `ready-for-human` |
| `wayfinder:grilling` | keeps its label and gains `ready-for-human` + `alex-grill` |
| `wayfinder:map` | keeps its label and gains `epic` |

Retired, and deleted once no issue carries them: `alex-supervised`, `alex-verify`, `design-ruling`, `copy-ruling`, `ralph-soon`, `paused`, `alex-other`, `root-session`, `good first issue`, `help wanted`, `invalid`.
