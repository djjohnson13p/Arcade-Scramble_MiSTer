# Agent Super Bond lab candidate

Hardware acceptance is in progress. This is a preserved lab candidate, not a completed fix or an upstream submission.

The change adds a dedicated mode20 (MRA byte14) for the unencrypted Super Cobra conversion. Coin, eight-way movement, separate Start1/Start2, Zap and stationary Hold shooting reach the game's expected input bits. Existing modes0–19 are unchanged. The new game MRA is under releases/. Its provisional palette follows the existing reference.

SB45F001.rbf and SB45F001.mra are the exact isolated hardware-test pair. Keep the normal Scramble installation while testing; the MRA uses its own SB45F001 name and matching RBF. The required game ROM ZIP is supplied separately by the user.

Quartus25.1 Lite compiled the candidate at the original intended clocks and seed. Eight-corner constrained-fabric minimum slacks: setup +0.346ns, hold +0.109ns, recovery +3.674ns, removal +0.379ns. Inherited HPS/off-chip I/O coverage gaps remain; this is not full-board timing signoff. Quartus changed only LAST_QUARTUS_VERSION metadata in the isolated QSF; raw conservative failure flags and the separate byte-level acceptance are preserved.

MANIFEST.json binds the exact compiled RTL byte copy, RBF and selected evidence. Git may normalize source line endings; compiled-Arcade-Scramble.sv preserves the exact compiled overlay bytes. Hardware acceptance and regression results will be recorded here after the remaining checks finish. No PR or author contact has been made.

Completed hardware checks so far: correct separate starts and alternating Player2 turn/scoring, all eight movement directions, gameplay sound, B plus direction stationary shooting and A Zap response; connected Coin1 gives the configured1/2/3/4 credits; five lives show four reserve icons before a death; Free Play starts without a coin; Invulnerable survives enemy contact; DemoOff preserves gameplay sound and silences normal post-game demo sound. Human observations supplement the captured frames.

`hardware-evidence-through-dips.zip` preserves the closed session journals, exact raw captures, fixture bindings, hardware review and helper sources. `hardware-evidence-index.json` binds all117 archived files. The archive also retains earlier stopped/inconclusive phases as history; a completed transport action alone is not a gameplay pass.

Still pending: normal-life progression and core Reset/restart, Player2 special/combined actions, post-game DemoOn audio, FreePlay restart, and Scramble/SuperCobra hardware regressions. The normal Super Bond game is left under the user's control for these observations.

The included hardware-review correction narrows the five-life evidence to four visible reserves before a death; the paired images do not establish the subsequent decrement. Five starting lives remains verified.
