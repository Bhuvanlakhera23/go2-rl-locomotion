# When numerical policy parity wasn't enough

## The engineering problem

I wanted to carry a learned blind Go2 policy from its training workflow into a
separate simulation runtime. Exporting the actor was one part of that work. A
second part was ensuring that the receiving system constructed observations,
maintained history and applied joint targets consistently. A policy can produce
the expected numbers for a supplied tensor while the complete control loop still
behaves poorly.

The blind high-obstacle locomotion policy export and MuJoCo investigation made this distinction concrete.
The numerical tests and the closed-loop test asked different questions. Their
results remain separate: an initial export-parity failure, a later narrowly
scoped parity pass, and a failed nominal walking qualification. None is a claim
that the robot is ready for hardware deployment.

## What numerical parity established

The first parity protocol compared native PyTorch actor outputs with the exported
TorchScript bundle. Across its 210 cases, matched-batch native/export error was
zero. However, its cross-batch comparison reached an absolute discrepancy of
1.1444091796875e-5, localized to `FR_calf_joint`. That exceeded the frozen 1e-5
tolerance, so **V1 remained FAIL**. The threshold was not relaxed after seeing the
result, and the later test did not turn those original cases into a pass.

A separately defined V2 protocol tested a frozen fixed-batch-1 CPU numerical
profile. It passed within that scope. The
meaning of that result is specific: output agreement under the tested input,
batching and backend conditions. It does not qualify variable-batch inference,
validate the simulation's observation construction or establish stable walking.

## What remained outside the numerical test

The tensor presented to an actor is produced by a runtime. Its meaning depends
on joint ordering, body-frame conventions, command interpretation, previous-action
feedback and the timing and ordering of history updates. After inference, action
scaling, default joint positions and the position-control interface determine
what reaches the simulated robot. Physics and contact dynamics then influence
the next observation.

These are possible places to investigate when transfer fails; listing them is
not a diagnosis of this run. Numerical agreement alone cannot establish that all
these parts jointly reproduce the intended feedback loop. It also cannot convert
a nominal walking check into evidence of high-step climbing or hardware safety.

## The bounded MuJoCo test

The retained R2 qualification tested closed-loop nominal walking. Scene compilation
and compiled-model assertions passed, so the run progressed beyond those setup
checks. The policy then executed in the loop until a frozen root-height limit
was crossed.

| Retained R2 observation | Value |
|---|---:|
| Simulated time at failure | 9.035 s |
| Completed control intervals | 451 |
| Policy-call attempts | 452 |
| Physics rows | 1,807 |
| Root height at failure | 0.179808457 m |
| Frozen minimum root height | 0.18 m |

The integrated root height fell below the minimum, and **MuJoCo R2 remained
FAIL**. A compiled scene and a running actor were necessary setup milestones;
they did not establish a successful locomotion transfer.

## Reading the failure without inventing a cause

The offline review observed height oscillations, posture deterioration and
substantial heading drift. These describe the recorded behavior. They do not
uniquely identify which observation, controller or dynamics difference caused it.
The review did not rerun the policy, select a different checkpoint or relax the
height gate to obtain a favorable outcome.

The useful diagnostic approach was to keep each layer's conclusion bounded:
check the export's numerical behavior, distinguish that from runtime-input
semantics, then examine the recorded closed-loop outcome against its original
criterion. Passing one layer does not remove a failure in another. The available
record supported localization of the observed deterioration, not a controlled
causal comparison among all possible interface or physics differences.

## What I learned

**Numerical output agreement under a bounded profile does not prove stable
closed-loop behavior across simulators.** The failed walking test is useful
engineering evidence precisely because it limits what I can claim from the
export-parity pass. The transfer problem remains unresolved; this case study
introduces no new test, repair or deployment qualification.

All numerical observations above are already published in the
[retained results and limitations](limitations.md#retained-negative-results).
The [architecture overview](architecture.md) explains the interface at a conceptual
level. This account adds no controller implementation, weights, raw telemetry or
new causal finding. **approved_for_actuation: false**.
