# What this showcase does not establish

## Simulation, hardware and benchmark scope

The 117/128 historical result is a detector-defined nominal simulation benchmark,
with one trained policy per condition and two evaluation seeds. It is not an
estimate of population-level training reliability. The historical reference is
not an equal-budget control. Video excerpts add no benchmark episodes.

The qualitative stair setup is author-described as 28 cm. It has no independently
adjudicated supported-traversal rate at that height. Owner sidecar values for the
other clips are configuration descriptions, not verified measurements of every
visible obstacle. The supplied physical Go2 recording has no established
checkpoint identity or synchronized command/condition record in this showcase.

## Retained negative results

**Export parity V1 remains FAIL:** the cross-batch maximum discrepancy was
1.1444091796875e-5 against a frozen 1e-5 tolerance, localized to FR_calf_joint.
Matched-batch native/export error was zero. V1's 210 cases are not reinterpreted.

**Export parity V2 remains scoped PASS:** only fixed batch 1 under the separately
frozen CPU numerical profile. This is not variable-batch qualification, simulation
observation validation or sim-to-real safety approval.

**MuJoCo R2 closed-loop qualification remains FAIL:** scene compilation and
compiled-model assertions passed. The owner-run policy executed for 9.035
simulated seconds, retaining 451 completed control intervals, 452 policy-call
attempts and 1,807 physics rows. Integrated root height reached 0.179808457 m,
below the frozen 0.18 m minimum. The offline review found height oscillations,
posture deterioration and substantial heading drift; no unique causal failure
mechanism was established. It did not rerun the policy or relax the gate.
An earlier unrelated MuJoCo recording found in the wider workspace is not evidence
that this failed Foundation-02B run passed.

## Reproduction, disclosure and safety

The historical generalist lineage is partly unresolved; the recovered July 8
fresh recipe does not reproduce the July 16 checkpoint. This results-only
repository is not a complete training pipeline. No weights, source implementation,
private logs, robot assets or controller are included.

Physical footage does not validate a public safety system. Hardware safety and
independent stopping remain unqualified. **approved_for_actuation: false.**
No transport, robot command or executable controller is present.

No training, export, policy inference, simulation or hardware test was executed
to build this showcase. Only retained data, CPU media processing and local
presentation checks were used. All original research decisions remain unchanged.
