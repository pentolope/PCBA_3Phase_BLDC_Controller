# Three-Phase BLDC Motor Controller

A 24 V three-phase BLDC motor controller for approximately 10 A continuous and 20 A short-duration peak phase current, with six external N-channel MOSFETs and CAN-FD.

This repository holds the design problem for a 24 V three-phase BLDC motor controller sized for approximately 10 A continuous phase current and 20 A short-duration peak. The brief fixes the power-stage architecture (six external N-channel MOSFETs driven by a three-phase gate driver), the control and sensing set (an MCU with motor-control timers, phase/bus current sensing, DC bus voltage sensing, encoder/Hall inputs) and the communications interface (CAN-FD). It also fixes layout intent rather than layout detail, and it draws its own line between obligation and preference: one sentence says the PCB must make the gate-drive and power-commutation loops explicit and compact, provide substantial copper for the phase/bus current, keep current-sense routing Kelvin and away from switching nodes, and provide a plausible thermal path; two further sentences say connectors for DC power and motor phases should sit near the power stage and that logic and communications should occupy a quieter region of the board. That must/should distinction is the brief's own and is preserved here. Everything below that level - specific devices, current-sense topology, auxiliary rail generation, protection strategy, switching parameters, connectors, board outline and stackup detail - is left to the design agent and is recorded here as an open decision, not a pre-made choice; the brief requires those choices to be made and documented rather than recast as hidden user requirements.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 17 requirements and deliberately leaves
20 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| DC bus voltage | 24 V | brief |
| Phase current rating | Approximately 10 A continuous, 20 A short-duration peak | brief |
| Power switches | Six external N-channel MOSFETs (three half-bridges) | brief |
| Gate drive | A three-phase gate driver | brief |
| Controller | An MCU with motor-control timers | brief |
| Sensing | Phase/bus current sensing and DC bus voltage sensing | brief |
| Current-sense routing rule | Kelvin routing, kept away from switching nodes | brief |
| Position feedback | Encoder/Hall inputs | brief |
| Communications | CAN-FD | brief |
| Power-loop geometry and copper | Gate-drive and power-commutation loops explicit and compact; substantial copper for phase/bus current | brief |
| Thermal path | A plausible thermal path is required; which devices it serves and how it is built are not specified | brief |
| Connector placement | DC power and motor-phase connectors should sit near the power stage (stated as a should, not a must) | brief |
| Board zoning | Logic and communications should occupy a quieter region of the board (stated as a should, not a must) | brief |
| Likely layer count | 4 | metadata |
| Device selection, board outline, stackup detail, auxiliary rails, protection | Not fixed by the brief - design agent's choice, to be made and documented as an engineering decision rather than presented as a user requirement | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 18 of 32 |
| Category | power-motor |
| Difficulty | 4 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 4 |
| Primary stressors | three half-bridges, gate-drive loops, phase-current sensing, thermal/high-current |

This is a power-motor board at difficulty 4/5 with a detail-4/5 brief: the brief states real architectural and layout intent, so under-capturing it is as much a failure as inventing beyond it. It stresses three half-bridges, gate-drive loops, phase-current sensing and thermal/high-current handling - the areas where a design agent must show physical evidence (loop area, copper cross-section, Kelvin sense returns, junction-temperature path) rather than assertions. The brief also distinguishes what the PCB must do from what placement and zoning should do, and that distinction is part of the specification rather than an accident of wording. What it deliberately does not fix - devices, sense topology, protection, rails, mechanical envelope - is where the benchmark tests whether the agent documents an engineering choice instead of fabricating a user requirement.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_3Phase_BLDC_Controller.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `d3eef382d8d91ccdb28d72d3f3a9c89a89e0ec95a4ba4f573bd68555a4eced59`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
