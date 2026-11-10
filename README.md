<h1 align="center">Go2 RL Locomotion</h1>
<p align="center"><strong>Blind reinforcement learning for quadruped locomotion and obstacle traversal</strong></p>
<p align="center">Bhuvan Lakhera · Research with Deepan Muthirayan</p>

<p align="center"><img src="media/hero/fixed-policy-stair-demonstration.gif" width="640" alt="Foundation-02B fixed-policy stair-climbing playback in simulation"></p>
<p align="center"><em>Selected simulation playback. The configured 28 cm setup is qualitative, not a measured 28 cm success rate.</em></p>

I built a staged reinforcement-learning pipeline for the Unitree Go2, from flat-ground
locomotion to blind obstacle traversal. The actor uses proprioception, commands and
motion history; a privileged critic supports learning during training. My work spans
simulation, policy training, evaluation, controller integration and physical robot
experiments. This showcase brings together what I built, what I measured and where
transfer remains unresolved.

- **Four stages:** flat → rough → generalist → high-obstacle locomotion.
- **117/128 historical completions** on the nominal 16–18 cm obstacle cohort.
- **Blind actor:** no terrain-height map in the actor's inference inputs.

[Results](#historical-high-obstacle-results) · [Architecture](#from-proprioception-to-action) ·
[Full gallery](docs/media-gallery.md) · [Technical report](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl)

This public repository contains results and presentation material. The complete
training implementation, controllers and trained weights are not distributed here.

## From basic locomotion to obstacle skills

| Stage | Objective | Evidence available here |
|---|---|---|
| Flat | Learn locomotion and command response | Training-stage context; no checkpoint-bound Stage 1 recording |
| Rough | Adapt to uneven terrain | Later fixed-policy terrain footage; not a Stage 2 checkpoint demonstration |
| Generalist | Combine terrain and stair behaviors | Historical progression; no independently identified Stage 3 clip |
| High-obstacle | Learn isolated-step and multi-riser traversal | Foundation-02B fixed-policy playback and its historical benchmark |

The recovered July 8 training recipe does not establish reproduction of the
historical July 16 generalist checkpoint. Later demonstrations do not independently
verify earlier stages. [Method and evidence boundaries](docs/methodology.md).

## Beyond regular stairs · simulation

![Fixed-policy playback over irregular rocky stairs](media/rough/fixed-policy-rocky-trail.gif)

Selected later fixed-policy playback on irregular terrain. My recording notes describe
variable stair geometry and teleoperation; this is a demonstration, not a scored
robustness test. Friction variation and separate-block footage are in the
[gallery](docs/media-gallery.md).

## Physical Go2 · block traversal

![Selected physical Go2 block pass with tether and handler visible](media/hardware/physical-block-alternate-pass.gif)

A selected physical recording with tether and handler visible. The retained media
does not bind this pass to an exact checkpoint, command stream or assistance record.
It demonstrates physical motion, not a measured hardware climbing frontier or
qualified Foundation-02B transfer. More [physical footage](docs/media-gallery.md#physical-go2)
includes pad-course motion and **behavior after loss of support**: the robot keeps
moving its legs and body, but does not self-right in the complete recorded sequence.

## Historical reference · simulation context

![Historical pretrained reference stair attempt](media/high-obstacle/historical-reference-stair-attempt.gif)

Selected playback of the historical Model5099 reference, not the adaptive sampler.
This and the hero clip illustrate different behavior; their commands and conditions
are not matched, so the videos are not a controlled comparison.
[Complete published recordings and context](docs/media-gallery.md#historical-reference).

## Historical high-obstacle results

<img src="media/figures/historical-completion.png" width="900" alt="Historical 16–18 cm completion counts: fixed 117/128, adaptive 47/128, historical reference 1/128">

| Original nominal evaluation | Fixed sampling | Adaptive sampling | Historical reference |
|---|---:|---:|---:|
| Combined 16–18 cm isolated / three-riser staircase | **117/128 · 91.4%** | 47/128 · 36.7% | 1/128 · 0.8% |
| Isolated 18 cm | **31/32** | 12/32 | 0/32 |
| Three-riser staircase 18 cm | **25/32** | 1/32 | 0/32 |

These are detector-defined first-episode completions: one training seed per
condition and two evaluation seeds, not independent PPO replications. The
historical reference is not an equal-training-budget control. Acquisition gains
coexist with ordinary-locomotion retention costs. Videos add no samples to these
denominators, and the 28 cm demonstration does not extend this benchmark.
[Results and sources](docs/results.md).

## From proprioception to action

<img src="media/figures/conceptual-architecture.svg" width="960" alt="Proprioception, commands and temporal context feed a blind actor; a privileged critic is used only for PPO training">

Motion history gives the actor temporal context. The asymmetric critic uses
privileged information during PPO training, outside the actor's inference inputs.
Foundation-02B continues the historical prior with a fixed terrain-task mixture.
[Conceptual architecture](docs/architecture.md).

I also worked on simulator-to-controller interfaces, observation/action contracts,
Unitree SDK2 and CycloneDDS integration, joint mapping and position-target control.
The older 48-observation controller stack is separate from the temporal Foundation-02B
interface; that experience does not establish a qualified safety system.

## Limits of the evidence

The strongest measured result here is a bounded simulation benchmark, not a claim
of reliable climbing across training seeds or physical robots. Numerical export
equivalence holds only for a fixed-batch-1 CPU profile. Closed-loop MuJoCo transfer
failed its minimum-height criterion; its cause remains unresolved. Selected hardware
footage does not establish policy identity, repeatability or deployment safety.

[Detailed limitations and retained negative results](docs/limitations.md) ·
[Verification scope](docs/verification.md).

## Research and attribution

**Bhuvan Lakhera and Deepan Muthirayan.** *Experience Allocation and
Acquisition–Retention Trade-offs in Blind Quadruped Obstacle Learning.*
Technical report, 2026; not a peer-reviewed conference publication.

[Technical report](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl) ·
[Frozen v1.1.0](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl/releases/tag/v1.1.0) ·
[Citation](CITATION.cff) · [Media rights](docs/rights.md).

Previously published report media retains CC BY 4.0 attribution. Other first-party
media has no new blanket reuse license. No actuation approval is granted.
