### 📝 Description
I worked with Codex to add the missing hardware configuration and MRA for the unencrypted Super Cobra conversion of Agent Super Bond. The dedicated input mode provides eight-way movement, separate player starts, Hold and Zap.

I tested the build on my first-generation dual-RAM MiSTer Pi and confirmed both players’ controls, Hold and Zap together, room progression and sound. We also verified DIP settings, Free Play, reset/restart behavior, and Scramble/Super Cobra regressions. The Quartus 25.1 build passes all eight available timing corners, with the inherited timing-coverage qualifications documented in the test report.

### 🔗 Related Issues
Closes #45.

### Validation
- The included dated RBF is the exact hardware-tested build. RTL modes0–19 and the issue’s ROM payload remain unchanged; new mode20 is selected by MRA byte14.
- Quartus25.1 Lite, eight-corner constrained-fabric minima: setup +0.346ns, hold +0.109ns, recovery +3.674ns, removal +0.379ns. Existing HPS/off-chip coverage limits remain; no timing constraints were relaxed.
- Production input-decode contracts and old-mode comparisons passed. Detailed build provenance, vector counts, hardware observations, binary hash and the declared provisional palette reference: [verification report](https://github.com/djjohnson13p/Arcade-Scramble_MiSTer/blob/0a5b4e5afdc12222650a584eaff9b813313db906/lab-artifacts/superbond-20261024/VERIFICATION.md).

Implementation and analysis were AI-assisted with Codex; the description was reviewed and approved by me, and live hardware observations were confirmed by me.

### ✅ Checklist
- [x] Changes follow the project’s existing mode and MRA style.
- [x] Code was self-reviewed with Codex and independently checked; hardware was tested by the contributor.
- [x] No code comments were added.
