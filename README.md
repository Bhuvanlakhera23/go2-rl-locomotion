<h1 align="center">Go2 RL Locomotion</h1>
<p align="center"><strong>From proprioceptive locomotion to blind obstacle traversal</strong></p>
<p align="center">Bhuvan Lakhera · Research with Deepan Muthirayan</p>

<p align="center"><img src="media/hero/fixed-policy-stair-demonstration.gif" width="640" alt="Blind high-obstacle locomotion policy climbing stairs in simulation"></p>
<p align="center"><em>Simulation playback in a configured 28 cm stair scene. This is a qualitative demonstration; the measured benchmark below covers 16–18 cm.</em></p>

I built a staged reinforcement-learning pipeline to investigate how far a Unitree
Go2 can progress using proprioception alone. Starting with basic locomotion, I
worked through rough terrain, mixed locomotion tasks and higher obstacles. The
blind actor uses joint and body observations, velocity commands and motion history,
without a terrain-height map in its inputs.

My implementation spans Isaac Lab environments, PPO training, evaluation, policy
export and runtime integration. The work also includes physical robot experiments.
A later MuJoCo experiment highlighted another challenge: matching the exported
policy's outputs numerically was not enough to guarantee stable closed-loop
locomotion in a different physics simulator.

## The measured high-obstacle result

<img src="media/figures/historical-completion.png" width="900" alt="Historical 16–18 cm completions: Fixed-Mixture Policy 117/128, Adaptive-Frontier Policy 47/128, historical reference 1/128">

| Historical nominal simulation evaluation | Fixed-Mixture Policy | Adaptive-Frontier Policy | Pretrained Reference |
|---|---:|---:|---:|
| Combined 16–18 cm isolated steps / three-riser staircases | **117/128 · 91.4%** | 47/128 · 36.7% | 1/128 · 0.8% |
| Isolated 18 cm | **31/32** | 12/32 | 0/32 |
| Three-riser staircase 18 cm | **25/32** | 1/32 | 0/32 |

A policy trained using a fixed task mixture acquired substantially more complete
traversals than a policy trained using the specified adaptive task sampler in this
study. Task sampling allocated training experience; the learned actor does not
perform task sampling during locomotion. These counts come from the original
supported-traversal detector, one training seed per condition and two evaluation
seeds. The historical reference did not receive an equal continuation-training
budget. [Results and evaluation details](docs/results.md).

## How I developed the pipeline

| Stage | Engineering objective |
|---|---|
| **1 · Flat-ground locomotion** | Establish stable movement and velocity-command tracking |
| **2 · Rough-terrain adaptation** | Develop foot placement and body control on uneven surfaces |
| **3 · Generalist locomotion** | Combine terrain and stair tasks with ordinary movement commands |
| **4 · High-obstacle continuation** | Learn complete isolated-step and multi-riser traversal while retaining general locomotion |

Each stage posed a different problem. Moving near an obstacle was not enough;
the later evaluation needed to distinguish supported climbing from partial
footholds or a robot that simply remained upright. I also tracked ordinary
locomotion, so a climbing gain could be examined alongside changes in tracking,
action variation and effort proxies.

## Architecture and engineering

<img src="media/figures/conceptual-architecture.svg" width="960" alt="Proprioception, commands and temporal context feed a blind actor; a privileged critic supports PPO training">

The temporal representation gives the actor context about recent motion. During
PPO training, an asymmetric critic receives privileged information that the actor
does not use at inference. I developed the staged simulation/training workflow,
evaluation and export interfaces around that separation.

Runtime integration brought another set of problems: observation packing, history
order, joint mapping, action scaling and position-target control. My work with
Unitree SDK2 and CycloneDDS involved an older **48-observation controller stack**;
that interface is separate from the later history-conditioned high-obstacle
system. [Architecture](docs/architecture.md) · [Training and media context](docs/methodology.md).

## On irregular terrain · simulation

![Blind high-obstacle locomotion policy on irregular rocky stairs](media/rough/fixed-policy-rocky-trail.gif)

Selected playback of the blind high-obstacle locomotion policy over irregular stairs. Friction variation and
separate-block recordings are in the [full gallery](docs/media-gallery.md).

## On the physical Go2

![Physical Go2 block pass with tether and handler visible](media/hardware/physical-block-alternate-pass.gif)

A selected physical block pass, with the tether and handler visible. It is a
hardware demonstration, not a scored simulation benchmark. The gallery also
shows pad-course motion and [behavior after loss of support](docs/media-gallery.md#behavior-after-loss-of-support),
where the robot continued moving but did not self-right.

## A historical reference · simulation

![Historical Model5099 reference attempting stairs](media/high-obstacle/historical-reference-stair-attempt.gif)

The historical Model5099 reference attempting stairs. This provides qualitative
context for the hero clip; the recordings are not a matched-command comparison.
[Complete published recordings](docs/media-gallery.md#historical-reference).

## What the experiments taught me

Harder-terrain exposure and learned climbing are different outcomes. The most
useful measure was completed traversal, considered together with ordinary
locomotion. For the policy trained using a fixed task mixture, acquisition gains
came with tracking and motion-cost trade-offs—one reason I treat retention as
part of the learning problem rather than a final check.

I investigate that question with **Deepan Muthirayan** in
[*Experience Allocation and Acquisition–Retention Trade-offs in Blind Quadruped
Obstacle Learning*](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl).
The technical report explains the matched continuation experiment, exposure
records and per-task counterexamples. [Report v1.1.0](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl/releases/tag/v1.1.0) ·
[Citation](CITATION.cff).

## Evaluation scope

The benchmark is a single-training-seed simulation study, not a hardware success
rate. Export equivalence passed only a fixed-batch-1 CPU protocol; closed-loop
MuJoCo walking failed its minimum-height criterion. Historical training-lineage
questions and hardware safety remain unresolved.
[Detailed limitations, including the retained parity and MuJoCo results](docs/limitations.md).
[Engineering case study: numerical parity and sim-to-sim transfer](docs/numerical-parity-and-sim-transfer.md).

## Code availability

The complete training implementation and trained policies are not publicly
distributed here. This repository focuses on demonstrations, measured results
and research documentation. [Media attribution and rights](docs/rights.md).
