# PCBA_3Phase_BLDC_Controller — Three-Phase BLDC Motor Controller
## Design brief

Design a 24 V three-phase BLDC controller for approximately 10 A continuous phase current and 20 A short-duration peak. Use six external N-channel MOSFETs, a three-phase gate driver, an MCU with motor-control timers, phase/bus current sensing, DC bus voltage sensing, encoder/Hall inputs, and CAN-FD. The PCB must make the gate-drive and power-commutation loops explicit and compact, provide substantial copper for the phase/bus current, keep current-sense routing Kelvin and away from switching nodes, and provide a plausible thermal path. Connectors for DC power and motor phases should sit near the power stage. Logic and communications should occupy a quieter region of the board.

## Functional requirements

- The MCU timers must give three complementary PWM pairs with hardware dead time, a fault input that forces the outputs inactive without firmware, and PWM-synchronised ADC triggering.
- Hall and incremental-encoder feedback must both be accepted, neither required for the other, selectable without rework.
- All six gates must be off from power-on through MCU reset, before firmware runs.
- CAN-FD must meet the ISO 11898-2 physical layer, including its common-mode range and 120 Ω bus impedance.

## Power stage and gate drive

- Declare the operating bus range and rate every bus-connected part above its maximum, with margin for switching overshoot and for bus rise under regeneration.
- Declare the peak as magnitude, duration and repetition interval; rate FETs, sense elements, copper, vias and contacts for it and for 10 A continuous, and bulk capacitance for the ripple current at rated phase current.
- Gate drive must supply the peak gate current the chosen FETs and gate resistance demand, decoupled at each driver supply pin, with a discharge path holding each FET off while the driver is unpowered, and driver undervoltage lockout.
- Dead time must exceed worst-case driver delay mismatch plus FET turn-off delay over the declared range; identify what sets it.

## Current and voltage sensing

- Phase sensing must cover the peak range in both directions without clipping and settle before the ADC sample point; bus sensing must scale the declared bus range, including maximum regeneration excursion, into the ADC input range.
- Sense elements must survive the peak without a value change that invalidates measurement, with self-heating at 10 A in the stated accuracy.
- Every sense element must be Kelvin-connected: the sense pair starts at the sense terminals, carries no load current, and references an analog return free of commutation current.

## Layout, copper and thermal

- Each commutation loop must close against an uninterrupted return path on the adjacent layer with its area stated, and each gate loop must be compact and comparable between high and low side.
- Phase and bus copper must hold a declared temperature rise at 10 A continuous, counted through vias, plane necks and pads rather than trace width alone.
- Sense pairs, feedback inputs, analog inputs and the CAN pair must not run under or beside phase, bus or gate nodes, nor reference copper carrying commutation current.
- Lossy devices must reach copper area or a mounting interface by an identified thermal path, under declared ambient, airflow and mounting conditions.

## Protection and fault response

- An overcurrent threshold above the declared peak and below the FET, driver and sense-element limits must disable all six gates in hardware, faster than the survivable time at that current.
- The fault state must be MCU-readable and require an explicit re-enable; it must not clear itself silently.
- Reverse DC input must be survived or mechanically prevented, shorts phase-to-phase and phase-to-rail must end in protected shutdown, and loss of a feedback signal must be detectable without producing an uncommanded output.

## Interfaces, connectors and test access

- Power and phase connectors must carry continuous and peak current per contact at their maximum temperature, be keyed against interchange, and be marked.
- The feedback connector must supply sensor power through filtered, ESD-protected inputs tolerant of any line shorted to sensor supply or return.
- CAN termination must be a fit option rather than permanently fitted, so the node can sit mid-bus.
- Probe grounds must sit beside each phase node and gate-drive supply, with measurable points for bus voltage, each rail, each sense output and the fault line, and a debug connector reachable with the stage energised.

## Open choices

- MCU family and package, against the timer, ADC and fault-input requirements above.
- Gate-driver architecture: bootstrap versus isolated or charge-pump high-side supplies.
- Current-sense method and channel count, and whether bus current is measured or derived.
- MOSFET technology and package, stackup and copper weight, outline and heatsink interface, and connector families.
- Source of the logic and gate-drive rails, and whether the CAN node is galvanically isolated.
