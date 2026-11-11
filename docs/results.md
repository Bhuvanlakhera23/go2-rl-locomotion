# Historical results, with the original denominators

The source is the frozen v1.1.0 technical report, §4.1 and its original nominal
fixture table. No new evaluation, policy selection or data reduction was performed
for the showcase. The small chart redraws the published counts without altering
the axes or denominator; [benchmark-counts.csv](benchmark-counts.csv) contains its values.

| Nominal fixture | Fixed-Mixture Policy | Adaptive-Frontier Policy | Pretrained Reference |
|---|---:|---:|---:|
| Isolated 16 cm | 30/32 | 22/32 | 1/32 |
| Isolated 18 cm | 31/32 | 12/32 | 0/32 |
| Three-riser 16 cm | 31/32 | 12/32 | 0/32 |
| Three-riser 18 cm | 25/32 | 1/32 | 0/32 |
| **Combined 16–18 cm** | **117/128** | **47/128** | **1/128** |

Fixed-Mixture Policy: 91.40625%; Adaptive-Frontier Policy: 36.71875%;
Pretrained Reference: 0.78125%.
The descriptive fixed–adaptive difference is 54.6875 percentage points. It is
not a population-level estimate of which algorithm trains better.

- Two evaluation seeds, 173 and 271; 16 assigned first episodes per fixture per
  seed. Each fixture totals 32 episodes; the four frontier fixtures total 128.
- Completion is defined by the original supported-traversal detector. A partial
  foothold/milestone is not full completion. Independent physical-contact truth
  was not established by the showcase or the selected recordings.
- One trained policy per condition. The historical pretrained reference is a
  different-budget reference, not a matched extra-training control.
- The published nominal protocol, geometry and termination interpretation stay
  attached to these results. No later protocol or clip is pooled with them.
- The qualitative recording described as 28 cm in my notes has no matched first-episode
  denominator and no independent per-riser/contact measurement. It does not
  establish a measured 28 cm climbing success rate.

Source: [public technical report](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl/blob/main/TECHNICAL_REPORT.md),
[frozen report tag](https://github.com/Bhuvanlakhera23/go2-obstacle-learning-rl/releases/tag/v1.1.0).
The existing report is unchanged. Source-document hashes are retained in
[the public-safe provenance record](media-provenance.json).
