# Architecture — Three-Phase BLDC Motor Controller

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- three half-bridges
- gate-drive loops
- phase-current sensing
- thermal/high-current

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## Power stage and device selection

- What MOSFET voltage rating gives adequate margin over the 24 V bus once phase-node ringing and any regeneration are accounted for?
- What conduction and switching loss does each device dissipate at 10 A continuous, and what does that become at the 20 A short-duration peak?
- How long is "short-duration" taken to be for the 20 A peak, and what evidence supports that interpretation?
- Which package is chosen, and how do its thermal and lead terminations interact with the substantial copper the brief requires for the phase/bus current?
- Are all six switches identical, and if not, why?
- What SOA and avalanche margin is claimed at the worst-case operating point?

## Gate drive and commutation loop geometry

- Where does the high-side gate-drive supply come from, and what does that choice imply for minimum and maximum duty cycle?
- How many distinct gate-drive loops does the chosen driver and return scheme create, what is the measured loop area of each on the layout, and how is each kept compact?
- What is the measured loop area of each power-commutation loop, and where does the high-frequency capacitance sit relative to each half-bridge?
- How is shoot-through prevented, and where does any dead time originate - the driver, the MCU timers, or both?
- What holds the gates off during power-up, brown-out and reset, before the MCU is driving?
- How symmetric are the three half-bridge layouts, and what happens to control accuracy if they are not?

## Current and voltage sensing chain

- What sensing method is used for phase current, and where in the circuit is the sense element placed?
- How is the Kelvin connection the brief requires physically realised at each sense element, and where does the sense return terminate?
- What is the shortest distance between any sense trace and a switching node, and what shields or separates them?
- What is the full-scale range of the sense chain, and does it still resolve usefully at the 20 A peak without clipping?
- When in the PWM cycle is the ADC sampled, and how is that synchronised to the timers?
- How is bus current sensing implemented, and does it share a chain with the phase sensing or stand separate?
- How is the DC bus voltage sense node attenuated, filtered and protected?

## Control, timing and position feedback

- Which timer resources on the chosen MCU generate the PWM for the three half-bridges, what modulation schemes do they support, and do they offer hardware dead-time insertion and an emergency shutdown input if the chosen scheme needs them?
- What is the switching frequency, and how was it chosen against MOSFET losses, current-sense settling and audible noise?
- How are Hall inputs and encoder inputs conditioned, and can both be populated at once or are they alternatives?
- What supply does the position sensor receive, and how is that supply protected against a miswired or shorted motor cable?
- What latency budget exists from current sample to PWM update, and does the chosen control scheme fit in it?
- How does the controller behave on loss of position feedback?

## Power distribution and auxiliary rails

- What rails does the board need beyond the 24 V bus, and what is each one's current budget?
- What converts 24 V down to the logic rails, and where is that converter placed relative to the switching nodes?
- How are the rails sequenced, and what happens to the gate drivers if a rail comes up late or sags?
- How much bulk capacitance sits on the 24 V bus, and what ripple current does it see at rated phase current?
- Is the analog sense supply separated from the digital supply, and how?

## Thermal path

- What junction temperature does each MOSFET reach at 10 A continuous, and by what calculation chain from device Rth to copper area to ambient?
- What ambient temperature and airflow assumption is the thermal claim made under, and is that assumption stated anywhere in the brief or chosen by the design?
- Which devices does the plausible thermal path serve - the MOSFETs alone, or also the gate driver, sense elements and any regulator?
- How much copper area and how many thermal vias serve each device, and on which layers?
- Does heat leave through the board copper alone, through a heatsink, or through a chassis interface, and what mechanical feature supports that?
- What temperature does the current-sense element reach, and what does that do to its accuracy and drift?
- How does the thermal solution interact with the preference that connectors sit near the power stage?

## Floorplan, zoning and stackup

- Where is the boundary between the power region and the quieter logic/communications region, and what crosses it?
- How are the DC power and motor-phase connectors placed so that phase copper stays short and wide?
- What layer count and copper weight is adopted, and does the phase copper cross-section meet the 10 A continuous requirement with acceptable temperature rise?
- How are the return paths on inner layers arranged so that switching return current does not run under the sense or logic sections?
- Do any signals from the logic region need to reach the power region, and how are they routed and referenced?
- What is placed directly beneath the switching nodes on other layers?

## Protection and fault behaviour

- What detects an overcurrent or phase-to-phase short, how fast does it act, and does the response path go through firmware or hardware?
- What happens on reverse polarity of the 24 V input, and is that a designed-for case?
- How is the bus protected during regeneration or a rapid deceleration that pushes energy back?
- What clamps or absorbs the phase-node overshoot, and what determines whether snubbers are needed?
- What is the safe state of the six MOSFETs on any detected fault, and how is the fault latched and cleared?
- What protection is applied to the CAN-FD and position-feedback lines, which leave the board on cables?

## Communications and external interfaces

- Where does the CAN-FD transceiver sit, and how does its placement relate to the quieter-region preference?
- Is bus termination on-board, selectable, or external, and what drives that decision?
- What common-mode and transient tolerance do the CAN lines need given the motor cabling in the same system?
- How is the CAN-FD pair routed relative to the phase copper and switching nodes?
- Is the node's identity or bit rate configurable, and by what mechanism?

## Mechanical and manufacturing

- What board outline, mounting pattern and keep-outs does the design commit to, and what drove them?
- What connector types are chosen for DC power and phases, and what is their current and temperature-rise rating relative to 10 A continuous?
- Does assembly need both sides populated, and what does that mean for the thermal path?
- Which fabricator capability class is assumed, and do the phase copper widths, thermal vias and minimum spacing fit inside it?
- What clearance is needed between the phase and bus copper and adjacent nets at 24 V, and which standard is cited to justify it?

## Verification and bring-up

- How is the board brought up safely at reduced bus voltage and current before running a motor?
- What test points expose the gate signals, sense outputs and rails without probing the switching nodes directly?
- How is each current-sense channel calibrated, and against what reference?
- What measurement demonstrates that the commutation loop is as compact as claimed - layout metric, simulation, or bench observation of phase-node ringing?
- What thermal measurement would confirm the claimed junction temperature at 10 A continuous?
- Which claims in this document remain unverified after bring-up, and how are they flagged?

## Answers still owed

All of them. See [status.md](status.md).
