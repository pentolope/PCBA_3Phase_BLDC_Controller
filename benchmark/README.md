# Benchmark entry — board 18 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_3Phase_BLDC_Controller` |
| Board id | `bldc_controller_3ph` |
| Category | power-motor |
| Difficulty | 4 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 4 |
| Primary stressors | three half-bridges, gate-drive loops, phase-current sensing, thermal/high-current |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

This is a power-motor board at difficulty 4/5 with a detail-4/5 brief: the brief states real architectural and layout intent, so under-capturing it is as much a failure as inventing beyond it. It stresses three half-bridges, gate-drive loops, phase-current sensing and thermal/high-current handling - the areas where a design agent must show physical evidence (loop area, copper cross-section, Kelvin sense returns, junction-temperature path) rather than assertions. The brief also distinguishes what the PCB must do from what placement and zoning should do, and that distinction is part of the specification rather than an accident of wording. What it deliberately does not fix - devices, sense topology, protection, rails, mechanical envelope - is where the benchmark tests whether the agent documents an engineering choice instead of fabricating a user requirement.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
