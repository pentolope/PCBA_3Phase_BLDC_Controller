# PCBA_3Phase_BLDC_Controller — Three-Phase BLDC Motor Controller

**Benchmark ID:** 18  
**Difficulty:** 4/5  
**Brief detail:** 4/5  
**Category:** power-motor  
**Likely layer count:** 4  
**Primary stressors:** three half-bridges, gate-drive loops, phase-current sensing, thermal/high-current

## Design brief

Design a 24 V three-phase BLDC controller for approximately 10 A continuous phase current and 20 A short-duration peak. Use six external N-channel MOSFETs, a three-phase gate driver, an MCU with motor-control timers, phase/bus current sensing, DC bus voltage sensing, encoder/Hall inputs, and CAN-FD. The PCB must make the gate-drive and power-commutation loops explicit and compact, provide substantial copper for the phase/bus current, keep current-sense routing Kelvin and away from switching nodes, and provide a plausible thermal path. Connectors for DC power and motor phases should sit near the power stage. Logic and communications should occupy a quieter region of the board.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
