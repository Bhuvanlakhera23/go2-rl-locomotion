# High-level architecture

![Conceptual blind actor and privileged critic](../media/figures/conceptual-architecture.svg)

**Inference:** proprioceptive observations and velocity commands → temporal motion
context → policy actor → joint commands → robot feedback. No actor terrain-height
map is required.

**Training only:** a critic uses privileged information for PPO value learning.
Its inputs and value output do not become deployed actor sensors or commands.

The project progresses from a locomotion prior through varied terrain and stair
behaviors to fixed-sampling high-obstacle continuation. This is a conceptual
research overview. The specialized actor/encoder source, reward coefficients,
terrain/curriculum generation, detector and deployment implementation remain
private and are deliberately absent from this repository.

No architecture illustration is evidence that the physical or MuJoCo deployment
has been qualified. See [limitations](limitations.md).
