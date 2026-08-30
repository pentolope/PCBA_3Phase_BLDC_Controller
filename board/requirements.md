# Requirements — Three-Phase BLDC Motor Controller

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `d3eef382d8d91ccdb28d72d3f3a9c89a89e0ec95a4ba4f573bd68555a4eced59`.

## Fixed by the brief

### REQ-01 — The board is a three-phase BLDC controller operating from a 24 V DC bus.

Brief text:

> Design a 24 V three-phase BLDC controller

### REQ-02 — It must support approximately 10 A continuous phase current with a 20 A short-duration peak.

Brief text:

> approximately 10 A continuous phase current and 20 A short-duration peak

### REQ-03 — The power stage uses six external N-channel MOSFETs.

Brief text:

> Use six external N-channel MOSFETs, a three-phase gate driver

### REQ-04 — The MOSFETs are driven by a three-phase gate driver.

Brief text:

> a three-phase gate driver, an MCU with motor-control timers

### REQ-05 — The board includes an MCU that has motor-control timers.

Brief text:

> an MCU with motor-control timers, phase/bus current sensing

### REQ-06 — The design includes phase/bus current sensing.

Brief text:

> phase/bus current sensing, DC bus voltage sensing

### REQ-07 — The design includes DC bus voltage sensing.

Brief text:

> DC bus voltage sensing, encoder/Hall inputs, and CAN-FD.

### REQ-08 — The design provides encoder/Hall inputs.

Brief text:

> DC bus voltage sensing, encoder/Hall inputs, and CAN-FD.

### REQ-09 — The board provides a CAN-FD communications interface.

Brief text:

> encoder/Hall inputs, and CAN-FD.

### REQ-10 — The PCB must make the gate-drive and power-commutation loops explicit and compact.

Brief text:

> The PCB must make the gate-drive and power-commutation loops explicit and compact

### REQ-11 — The PCB must provide substantial copper for the phase/bus current.

Brief text:

> provide substantial copper for the phase/bus current

### REQ-12 — The PCB must keep current-sense routing Kelvin and away from switching nodes.

Brief text:

> keep current-sense routing Kelvin and away from switching nodes

### REQ-13 — The PCB must provide a plausible thermal path.

Brief text:

> and provide a plausible thermal path

### REQ-14 — Connectors for DC power and motor phases should sit near the power stage. The brief states this as a should, not as one of its must clauses.

Brief text:

> Connectors for DC power and motor phases should sit near the power stage.

### REQ-15 — Logic and communications should occupy a quieter region of the board. The brief states this as a should, not as one of its must clauses.

Brief text:

> Logic and communications should occupy a quieter region of the board.

### REQ-16 — The repository should remain a consumer of the shared PCBA_AutoDesignAndTest toolkit rather than accumulating board-specific logic in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

### REQ-17 — Stated requirements are authoritative; where the brief leaves a choice open, the design agent must make and document a reasonable engineering decision rather than invent a hidden user requirement.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

## Open — the design agent decides

### OPEN-01 — Selection of the six N-channel MOSFETs: voltage and current rating, package, RDS(on) versus gate-charge trade-off, and avalanche/SOA margin.

The brief fixes only the count, type and external placement of the switches; it names no device, package or rating.

*Decision:* **not yet made.**

### OPEN-02 — Selection of the three-phase gate driver and the drive architecture around it (bootstrap versus separately supplied high side, integrated versus external dead-time control, which built-in protection features are relied on, and how many distinct gate-drive loops the chosen scheme creates).

The brief requires "a three-phase gate driver" and says nothing about its supply scheme, features or part.

*Decision:* **not yet made.**

### OPEN-03 — Gate-drive parameters: gate drive impedance and any gate resistor values, turn-on/turn-off asymmetry, dead time, and any gate clamping or pull-down for safe start-up.

The brief constrains the physical loop but states no switching or gate-drive numbers.

*Decision:* **not yet made.**

### OPEN-04 — MCU selection: family, core, package, memory, peripheral count, and debug/programming interface.

The brief requires only "an MCU with motor-control timers" and names no device or vendor.

*Decision:* **not yet made.**

### OPEN-05 — Current-sense topology: shunt versus magnetic sensing, low-side versus in-line/high-side placement, how many phases are individually sensed, whether phase and bus current are measured by separate chains or derived from a shared one, sense element value and power rating, and the amplifier or integrated sensor used.

The brief mandates "phase/bus current sensing" and a Kelvin routing rule, but not the sensing method, placement or channel count, and does not expand its own phase/bus shorthand.

*Decision:* **not yet made.**

### OPEN-06 — DC bus voltage sense implementation: attenuation method and ratio, filtering, ADC scaling and any protection on that node.

The brief requires DC bus voltage sensing but specifies no measurement range, accuracy or implementation.

*Decision:* **not yet made.**

### OPEN-07 — Encoder and Hall interface details: whether both are populated simultaneously or treated as alternatives, connector, sensor supply and its current budget, single-ended versus differential encoder support, level shifting, input filtering and protection, and channel count.

The brief names "encoder/Hall inputs" as a requirement without defining the electrical interface or resolving whether its slash means both together or either one.

*Decision:* **not yet made.**

### OPEN-08 — CAN-FD implementation: transceiver choice, bit rates, termination strategy, bus connector, common-mode/ESD protection, and whether isolation is used.

The brief names the interface only; it states no data rate, connector, topology or isolation requirement.

*Decision:* **not yet made.**

### OPEN-09 — Auxiliary rail generation: how logic, analog and gate-drive supplies are derived from the 24 V bus, their voltages, topology (switching versus linear), sequencing and current budget.

The brief is silent on internal rails; it fixes only the 24 V bus.

*Decision:* **not yet made.**

### OPEN-10 — DC-link and decoupling capacitance: bulk capacitance value and technology, ripple-current budget, and placement relative to the half-bridges.

The brief demands compact commutation loops but states no capacitance, ripple or ESR requirement.

*Decision:* **not yet made.**

### OPEN-11 — Protection strategy: overcurrent and short-circuit response and its speed, reverse-polarity protection, overvoltage/regeneration handling, fault latching and recovery, and any thermal shutdown.

The brief specifies sensing but names no protection function, threshold or response behaviour.

*Decision:* **not yet made.**

### OPEN-12 — Commutation and control scheme (trapezoidal, sinusoidal or field-oriented), PWM/modulation scheme and switching frequency, and the extent of firmware in scope.

The brief specifies motor-control timers and position-feedback inputs but not the control algorithm, modulation scheme or switching frequency.

*Decision:* **not yet made.**

### OPEN-13 — Thermal path implementation: which devices the path is built for, copper area and weight devoted to them, thermal via pattern, whether a heatsink or chassis coupling is used, airflow assumption, ambient range and allowed temperature rise.

The brief asks for "a plausible thermal path" without naming what it serves, and leaves every quantitative thermal target and mechanism unstated.

*Decision:* **not yet made.**

### OPEN-14 — Board outline, dimensions, mounting-hole pattern, keep-outs and any enclosure or heatsink mechanical interface.

The brief gives placement preferences but no dimensions, shape or mechanical envelope.

*Decision:* **not yet made.**

### OPEN-15 — Stackup detail: whether the metadata's likely 4 layers is adopted, copper weights, dielectric thicknesses and plane assignment.

The layer count is a benchmark metadata hint, not a stated requirement, and the brief fixes no copper weight or stackup.

*Decision:* **not yet made.**

### OPEN-16 — Connector selection for DC power, motor phases, encoder/Hall and CAN: type, current and temperature rating, orientation and part numbers.

The brief expresses only a preference for where the DC power and motor-phase connectors sit, not what they are.

*Decision:* **not yet made.**

### OPEN-17 — Grounding and return strategy: partitioning of power return, gate-drive return, analog sense return and logic ground, plane splits, and the star or single-point connection.

The brief requires Kelvin sensing and prefers a quiet logic region but does not define the ground architecture that achieves them.

*Decision:* **not yet made.**

### OPEN-18 — Input EMI filtering and switching-noise containment on the 24 V input and motor phases, and any snubbing at the half-bridges.

The brief is silent on EMC targets, filtering and snubbers.

*Decision:* **not yet made.**

### OPEN-19 — Test, bring-up and calibration provisions: test points, programming interface, status indicators, current-sense calibration method and safe low-power bring-up path.

The brief states no test or manufacturing-test requirement.

*Decision:* **not yet made.**

### OPEN-20 — Fabrication and assembly targets: fabricator capability class, single- versus double-sided assembly, minimum trace/space and via rules adopted, and which current-capacity standard is cited to justify them.

The brief names no fabricator, process, standard or manufacturability constraint.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Answer it under its `OPEN-nn` heading above, with the reasoning and the
   evidence that made the choice.
2. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json).
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Claiming a "plausible thermal path" without any junction-temperature chain - device dissipation, Rth, copper area, via count, ambient - is the single easiest thing to fake on this board.
- Asserting compact commutation and gate-drive loops without reporting an actual loop area or showing the current path on the layout; the brief demands the loops be explicit, which means demonstrable.
- Naming a specific MOSFET, gate driver, MCU, transceiver, connector or standard as if the brief required it. The brief names no part, vendor, package or external document anywhere.
- Inventing electrical numbers the brief never states: switching frequency, dead time, gate resistance, logic rail voltages, bus capacitance, PWM resolution, CAN bit rate. These are choices to be justified, not requirements to be quoted.
- Declaring Kelvin sensing while the sense return shares copper with the power return, or while sense traces pass over or under a switching node on an adjacent layer.
- Assuming a control algorithm (FOC versus trapezoidal) or a modulation scheme is mandated, or restating the brief's three "should" sentences - connector placement, logic/communications zoning, toolkit consumption - as hard constraints. The brief uses "must" in exactly one sentence, and fixes the feedback inputs and timer capability rather than the commutation scheme.
- Treating the metadata hint "likely layer count: 4" as a specification, or presenting a layer count as a finished stackup without copper weights and plane assignment.
- Sizing phase copper from a rule of thumb rather than from the 10 A continuous figure with a stated temperature rise and a citable current-capacity source.
