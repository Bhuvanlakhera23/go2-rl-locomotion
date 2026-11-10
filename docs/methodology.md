# Training progression and evidence boundaries

This portfolio describes a staged research program: flat locomotion, rough
terrain adaptation, generalist/stair locomotion, then fixed-sampling high-obstacle
continuation. It shares high-level architecture and existing results, not a
reproducible training implementation or complete experimental configuration.

The actor is blind to terrain-height maps and uses proprioception, motion history
and velocity commands. An asymmetric critic receives training-only privileged
information. PPO is the learning method. The high-obstacle study investigates how
experience allocation affects acquisition and retention; its original measured
fixed-sampling result is preserved separately from qualitative demonstrations.

## What each kind of evidence establishes

| Evidence | Appropriate interpretation | Does not establish |
|---|---|---|
| Frozen evaluation counts | Original detector-defined performance under that protocol | Hardware reliability, many-seed learning reliability or new height capability |
| Selected simulation excerpt | Authentic selected playback from the supplied recording | A complete evaluation, matched comparisons or independent checkpoint binding |
| Recording notes | My setup/policy description | Independent geometry, command-log or checkpoint-to-video verification |
| Physical Go2 excerpt | Authentic physical robot motion | Foundation-02B identity, high-step transfer or hardware safety qualification |
| Numerical parity | Equivalence within the separately frozen batch-1 CPU profile | Correct simulation observations or stable closed-loop behavior |

No exact Stage 1, Stage 2 or historical generalist checkpoint-bound demonstration
was established during media review. Later fixed-policy rough/stair clips remain
labeled as that later policy. Missing footage is not replaced with third-party
clips, synthetic robot imagery or an unrelated policy.

The recovered July 8 fresh recipe is not the historical July 16 generalist
checkpoint's exact reproduction. Its full-state resume lineage remains partly
unresolved. The historical Foundation-02B result retains its own original source
and checkpoint provenance; this showcase does not make a new reproduction claim.

Selected excerpts are not time-scaled, interpolated or stitched during showcase
preparation. Some newly supplied hardware originals already contain split-screen
views; their synchronization is unverified, and they are explicitly labeled. Display frame
rates and GIF delay rounding are documented. Clips loop with a reset to their
start; no seamless continuity across the loop boundary is claimed.
