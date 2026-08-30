# Sources — Three-Phase BLDC Motor Controller

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Power MOSFET datasheet | RDS(on) over temperature and gate voltage, gate charge, SOA and avalanche limits, and package thermal resistance - needed to justify the 10 A continuous / 20 A peak claim. |
| Three-phase gate driver datasheet | Supply and bootstrap requirements, peak sink/source current, propagation delay matching, dead-time and shoot-through protection behaviour. |
| MCU datasheet and reference manual | Motor-control timer capability (PWM generation, dead-time insertion, break/emergency input), ADC trigger and conversion timing, encoder interface, CAN-FD peripheral, and package thermal data. |
| Current-sense element and sense-amplifier datasheets, for the sensing method chosen | Shunt or magnetic-sensor tolerance and temperature coefficient, common-mode range, bandwidth and settling, and the manufacturer's Kelvin connection guidance for the element used. |
| CAN / CAN-FD specification and transceiver datasheet | The brief names CAN-FD; bit timing, bus levels, termination and stub constraints, plus transceiver common-mode and fault tolerance. |
| Fabricator capability and stackup documentation | Minimum trace/space, copper weight options, via and thermal-via rules for the adopted layer count, and the achievable phase-copper cross-section. |
| PCB current-capacity and thermal derating guidance | Trace width, copper area and temperature rise for the stated phase and bus currents, and clearance guidance at the 24 V bus; which current-capacity standard is adopted and cited is the design agent's choice to make and justify. |
| Bulk and ceramic capacitor datasheets | Ripple-current rating, ESR/ESL and DC-bias derating for the DC-link and half-bridge decoupling that set commutation loop performance. |
| Connector and terminal datasheets | Current rating, temperature rise, wire gauge accommodation and mating cycles for the DC power and motor-phase connections placed at the power stage. |
| Position-sensor interface documentation (Hall sensor and encoder) | Supply, output type and level, cable-length and filtering expectations for the encoder/Hall inputs the brief requires. |
| Thermal analysis evidence (calculation, simulation or measurement) | The brief requires a plausible thermal path; the junction-temperature chain from device dissipation through copper and vias to ambient must be shown, not asserted. |
| Shared PCBA_AutoDesignAndTest toolkit documentation | The repository should remain a toolkit consumer, so its configuration and check interfaces are the reference for how this board is built and validated. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
