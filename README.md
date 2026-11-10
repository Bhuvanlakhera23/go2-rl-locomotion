<h1 align="center">Go2 RL Locomotion</h1>
<p align="center"><strong>Blind Reinforcement Learning for Robust Quadruped Locomotion and High-Obstacle Traversal</strong></p>
<p align="center">Bhuvan Lakhera · Research with Deepan Muthirayan</p>

<p align="center">
  <img src="media/hero/fixed-policy-stair-demonstration.gif" width="800" alt="Selected Foundation-02B fixed-policy stair playback in simulation">
</p>

<p align="center"><em>Selected simulation playback, not a benchmark episode. The author-described 28 cm setup is qualitative; it is not a measured 28 cm capability claim.</em></p>

A research portfolio following a Unitree Go2 from basic locomotion to blind
high-obstacle learning. The work combines staged reinforcement learning,
proprioceptive temporal context and an asymmetric training critic, then examines
where learned capability holds—and where transfer fails.

- **Four-stage progression:** flat → rough → generalist → high-obstacle.
- **117/128 historical completions** on the nominal 16–18 cm obstacle cohort.
- **Blind inference:** proprioception and commands, without an actor terrain-height map.
- **Authentic demonstrations:** simulation playback and separately labeled physical Go2 footage.

<p align="center">
  <a href="#historical-high-obstacle-results">Results</a> ·
  <a href="#simulation-gallery">Demonstrations</a> ·
  <a href="#from-proprioception-to-action">Architecture</a> ·
  <a href="https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl">Technical report</a>
</p>

> **Results-only showcase, prepared locally for owner review.** The private training,
> curriculum, model and deployment implementations—and all weights—are excluded.
> No public deployment or hardware safety approval is implied.

## A progression of capabilities

| Stage | Research objective | Evidence shown here |
|---|---|---|
| **01 · Flat** | Establish basic locomotion and command response | Training-stage context; no checkpoint-bound Stage 1 video identified |
| **02 · Rough** | Adapt locomotion to varied terrain | Later fixed-policy terrain demonstrations below; not footage proving the Stage 2 checkpoint |
| **03 · Generalist** | Combine terrain and stair behaviors | Historical progression documented; no independently identified generalist-stage clip selected |
| **04 · High-obstacle** | Learn complete isolated-step and multi-riser traversal | Foundation-02B fixed-policy playback and the original numerical benchmark |

The recovered July 8 fresh-training recipe has **not** reproduced the historical
July 16 generalist checkpoint. The historical benchmark belongs to its original
lineage. This portfolio does not relabel later footage as earlier-stage evidence.
[Progression and evidence boundaries](docs/methodology.md).

## Simulation gallery

<table>
<tr>
<td width="33%"><img src="media/high-obstacle/separate-block-playback.gif" width="640" alt="Fixed-policy simulation playback across separated blocks"><br><strong>Separate obstacles</strong><br>Exploratory block-course playback. Blocks return to ground between obstacles; this is not a cumulative staircase. Terminations were disabled according to the owner notes.</td>
<td width="33%"><img src="media/rough/fixed-policy-rocky-trail.gif" width="640" alt="Fixed-policy simulation playback on rocky stairs"><br><strong>Irregular terrain</strong><br>Selected rocky-stair playback by the later fixed policy. Terrain and teleoperation notes describe the setup; this is not a scored robustness result.</td>
<td width="33%"><img src="media/rough/fixed-policy-friction-tiles.gif" width="640" alt="Fixed-policy simulation walking over randomized friction tiles"><br><strong>Friction variation</strong><br>Selected playback across labeled friction tiles, with owner-described observation noise. A qualitative example, not a measured robustness score.</td>
</tr>
</table>

**What to watch:** obstacle negotiation, motion over irregular geometry and gait
across changing surface conditions. These show distinct behaviors by the later
fixed policy; they do not establish the earlier-stage checkpoints.

All loops are short excerpts at the original timeline speed, with frame-rate
reduction for display. They are not complete evaluations or matched comparisons.
The [extended gallery](docs/media-gallery.md) includes friction-tile playback,
the historical reference attempt and an authentic stair still. It also links the
previously published full recordings; new full-video hosting remains pending.

## Historical high-obstacle results

<img src="media/figures/historical-completion.png" width="900" alt="Historical nominal 16–18 cm completion: fixed 117 of 128, adaptive 47 of 128, reference 1 of 128">

| Original nominal evaluation | Fixed sampling | Adaptive sampling | Historical reference |
|---|---:|---:|---:|
| Combined 16–18 cm isolated / three-riser staircase | **117/128 · 91.4%** | 47/128 · 36.7% | 1/128 · 0.8% |
| Isolated 18 cm | **31/32** | 12/32 | 0/32 |
| Three-riser staircase 18 cm | **25/32** | 1/32 | 0/32 |

These are **detector-defined first-episode completions**, with one trained policy
per condition and two evaluation seeds. Evaluation seeds do not replicate PPO
training. The historical reference is not an equal-training-budget control.
Selected GIFs add no samples to these denominators, and the qualitative 28 cm
footage does not extend this benchmark. [Results, denominators and sources](docs/results.md).

## From proprioception to action

<img src="media/figures/conceptual-architecture.svg" width="960" alt="Proprioception and commands pass through temporal context and a blind policy actor to joint targets; a privileged critic is used only during training">

Recent motion history gives the actor temporal context. A privileged critic
supports value learning during PPO training while remaining outside the actor's
inference inputs. The staged research culminates in Foundation-02B's fixed-
sampling high-obstacle continuation. This diagram explains the idea; it does not
release network internals, specialized rewards, curriculum code or controllers.
[Architecture overview](docs/architecture.md).

## Emergent recovery attempt · physical Go2

<p align="center"><img src="media/hardware/emergent-recovery-attempt.gif" width="720" alt="Complete supplied physical Go2 clip showing loss of footing, active leg and body motion, and an ending with the robot still down"></p>

A short, interesting response when the support surface shifts: the robot continues
moving its legs and body after losing footing. This is the **complete supplied
visual sequence**, at the original timeline speed, rather than a success-only cut.

“Emergent recovery” is the owner's description. **The clip ends with the robot
still down; it does not demonstrate successful self-righting.** It motivates a
research question about the learned response, without establishing its training
mechanism or repeatability. Watch the body reorientation, continuing leg motion
and displacement of the loose pads. [Sequence frames and context](docs/media-gallery.md#emergent-recovery-attempt).

## Physical Go2 footage · separate evidence

<table>
<tr>
<td width="50%"><img src="media/hardware/physical-block-alternate-pass.gif" width="640" alt="Owner-approved physical Go2 block playback with tether visible"><br><strong>Block pass</strong><br>A different recorded pass, selected for more fluid progression across the block; tether and handler remain visible.</td>
<td width="50%"><img src="media/hardware/physical-pad-course.gif" width="640" alt="Owner-supplied split-screen physical Go2 recording on foam pads"><br><strong>Pad-course playback</strong><br>Supplied split-screen recording; synchronization of its views is unverified.</td>
</tr>
</table>

Selected motion from owner-approved physical Go2 recordings. Exact checkpoints,
command streams, assistance and run conditions are not established by the retained
media records. Visible tethers are preserved; no unassisted-traversal claim is made.
These are qualitative physical-motion observations, not a measured hardware
climbing frontier or Foundation-02B transfer qualification. See
[hardware caption boundaries](docs/media-gallery.md#physical-go2).

## What remains unvalidated

- **MuJoCo R2 closed-loop qualification: FAIL.** Scene compilation/model assertions
  passed, but execution stopped at **9.035 simulated seconds** when root height
  crossed the frozen minimum. Height oscillations, posture deterioration and
  heading drift were observed; no unique cause was established.
- **Export parity:** V1 remains FAIL; V2 passed only its frozen batch-1 CPU numerical
  profile. Numerical equivalence does not establish closed-loop transfer.
- **Reproduction and safety:** historical lineage remains partly unresolved;
  selected physical footage is not safety approval. `approved_for_actuation: false`.

[Detailed limitations](docs/limitations.md) · [Media provenance](docs/media-provenance.json).

## Research and citation

[Technical report and evidence](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl) ·
[Frozen report v1.1.0](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl/releases/tag/v1.1.0) ·
[Citation](CITATION.cff).

**Bhuvan Lakhera and Deepan Muthirayan.** *Experience Allocation and
Acquisition–Retention Trade-offs in Blind Quadruped Obstacle Learning.*
Technical report, 2026. No peer-reviewed publication status or software DOI is claimed.

This repository contains presentation material only. Previously published report
media retains its CC BY 4.0 attribution; other first-party media is included under
the owner's stated approvals without assigning a new blanket license.
[Rights and disclosure scope](docs/rights.md) · [Local verification](docs/verification.md).
