# Agent Super Bond verification

The selected fix fully addresses [issue45](https://github.com/MiSTer-devel/Arcade-Scramble_MiSTer/issues/45): the missing hardware/input configuration for the **unencrypted Super Cobra conversion**. The issue requests a dedicated `mod_superbon`, `hwsel=2`, eight-way movement and both Hold/Zap buttons. The issue's ROM composition remains unchanged (57,376 bytes; MD5 `f65f589945276dc75b001d59182aba4d`).

## Change and reproduction

The official core and an unchanged local Quartus25.1 build reproduced the faulty controls: Start1 did not start the game, while Fire2 did. The new mode20 (`14` in the MRA) supplies active-low Coin, eight directions, separate Start1/Start2, Zap and Hold at the game's expected PPI bits. Its MRA labels A=Zap and B=Hold. Modes0–19 retain their existing decode behavior. The upstream source base is `dea71c93615030583b23362226708f67d2294458`.

## Automated checks

The production RTL decode and joystick/PPI paths were extracted and checked with Icarus:16,384 new-mode control vectors across four controller transports;524,288 DIP cases;983,040 existing-mode comparisons;40,960 independent joint-port comparisons;3,760 invalid-mode comparisons. Compile and simulation exited0. MRA parsing, all required ROM CRC/size pairs, unchanged payload composition and the declared palette remark were checked. The archived verifier retains its original workspace path assumptions; it is preserved as evidence, without claiming a standalone installation.

## Quartus25.1 build and timing

Quartus25.1std.0 Build1129 Lite, original intended clocks and seed1,5CSEBA6U23I7. Native full flow completed normally in2702.281s, exit0. Fit uses39,236/41,910 ALMs (94%); unchanged baseline used39,582. No wall-clock cutoff, new clock exception or relaxed timing constraint was used. The25.1 build adapter provided `sys/pll_q25.qip` as a byte-identical alias of the supplied Q17 PLL list (`pll_q17.qip`); no PLL parameters changed. The alias is preserved here for reproduction, while the PR retains the original project configuration.

Saved-fit STA checked all eight available corners,14 clocks per corner. Minimum global constrained-fabric slacks:

| Check | Minimum slack |
|---|---:|
| Setup | +0.346ns |
| Hold | +0.109ns |
| Recovery | +3.674ns |
| Removal | +0.379ns |

All32 global checks have positive worst slack and zero violated paths. Minimum-pulse-width summaries/details agree without reported violations. The224 zero-path/NA clock rows are not counted as passes. No ignored SDC constraints were found.

**Coverage qualification:** this is constrained clocked-fabric timing acceptance, not full-board electrical signoff. Inherited coverage counts remain no_clock3094 (five HPS primitive groups, zero emu nodes), multiple_clock86, virtual_clock1, no_input_delay29 and no_output_delay129. Waveforms, periods and zero-path applicability match the unchanged baseline.

Quartus changed only QSF `LAST_QUARTUS_VERSION` from17.0.2 to25.1std.0. Raw exact-input/adapter failure flags and scheduler exit1 remain in the original receipt; a separate exact-byte review accepts that sole metadata change. All other132 protected inputs and all clock/constraint/seed/logic assignments remained unchanged. The saved-fit analysis used a separate database copy; its auxiliary cache changes are recorded, while all608 original completed-build files remained unchanged.

## Hardware acceptance

First-generation dual-RAM MiSTer Pi. The contributor watched/listened, operated the controller for live checks, and confirmed the following together with captured/managed tests:

| Behavior | Result |
|---|---|
| Boot; Coin; correct Start1; weapons do not start a game | Pass |
| Eight movement directions and normal directional shooting | Pass |
| Alternating two-player start, actual Player2 turn, controls and separate scoring | Pass |
| B plus direction gives stationary shooting; A invokes Zap | Pass |
| Hold plus Zap plus direction together | Live contributor confirmation |
| Normal-life room exit/progression | Pass; raw captures show Rooms2 and3 |
| Gameplay sound; post-game Demo Sounds On and Off | Live contributor confirmation |
| One Coin grants the configured1/2/3/4 credits | Pass; numeric credit captures |
| Three lives, five lives, Invulnerable, FreePlay | Pass; five lives show four reserves before death; Invulnerable contact survival confirmed live |
| Core Reset and no-coin FreePlay restart | Managed named Reset/Enter/Start1 chronology, with no Coin in the FreePlay leg; actual gameplay confirmed live |
| Scramble and SuperCobra existing-game regressions | Both players' movement, gunfire, bombs and sound confirmed; Reset/fresh starts checked |

Sparse instruction/black frames do not establish the final combo or FreePlay gameplay. Those conclusions use the contributor's explicit live reports. The five-life paired frames establish four reserve icons; a later decrement is not claimed from that pair. The independent final audit verified32 raw capture hashes and61 completed managed actions across the final two sessions. All sessions closed cleanly under User control; protected original/staged files and local bindings were unchanged.

## Reference qualification and artifacts

The supplied palette PROM remains provisional, as in the issue's ROM/reference. The new MRA declares it; this change does not claim recovery of the undumped original PROM. The reported issue is the missing configuration for the named unencrypted set; no encrypted-set or new hiscore support is claimed.

The tested RBF is exactly3,511,684 bytes, SHA256 `1f5c0768026ef96b8bdad31e1bb4ce490f90aabc458351896f1b9546dbec2400`. The proposed dated release RBF contains those exact bytes. `SB45F001.rbf` and `SB45F001.mra` are the isolated test pair. The exact compiled RTL overlay is preserved as `compiled-Arcade-Scramble.sv`; Git can normalize source line endings.

[Root acceptance](ROOT-FINAL-ACCEPTANCE.json), [independent hardware audit](INDEPENDENT-FINAL-HARDWARE-AUDIT.json), [timing review](timing-review.json), [final evidence index](hardware-evidence-final-index.json), and [raw evidence archive](hardware-evidence-final.zip) retain the underlying evidence. Earlier draft/through-DIP records are historical checkpoints superseded by final acceptance. No ROM ZIPs are included.
