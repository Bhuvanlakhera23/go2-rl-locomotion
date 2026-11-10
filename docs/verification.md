# Local owner-review verification

**SHOWCASE_READY_FOR_OWNER_REVIEW** — not authorization to publish.

The showcase was built in a new directory with independent Git history. The
private engineering repository, report, original media and research decisions
are unchanged. No policy, simulator, training, export, robot interface or GPU
video processing was executed. Media conversions use CPU FFmpeg.

Ten bounded CPU checks passed: derivative identities, GIF decoding/timing/motion,
image/SVG integrity, links/anchors, restricted-disclosure scan, benchmark counts,
original media preservation, private source preservation, caption/alt-text boundaries
and citation/rights scope.

## Media and presentation

- The expanded primary collection contains 13 videos and 12 analysis images,
  plus four simulation notes. The wider inventory contains 471 media files and
  288 unique SHA256 identities. Editing-project files were inventoried separately
  and are excluded from the showcase. Original paths and metadata remain in a private
  inventory outside this repository; only selected public-safe provenance is here.
- Nine continuous-excerpt GIFs are selected. The stair hero is 800 px wide; other
  loops are 640 px. Display rates are 12 fps, except physical footage at 10 fps.
  Durations are 7.01 s for the simulation GIFs and 3.50–6.00 s for physical footage;
  the 0.01 s difference from the source span is GIF centisecond-delay rounding.
- Each GIF is below 10 MB. Durations, decoded frame counts, dimensions, hashes,
  metadata and representative beginning/middle/end frames were checked. GIFs
  intentionally loop to their start; no seamless wrap or full-evaluation claim
  is made. Audio is omitted; source audio/metadata remain untouched privately.
- A real source frame is resized to an 800 px PNG. A factual PNG chart and a conceptual SVG illustrate
  the published counts and conceptual actor/critic separation. No synthetic
  robot-performance image or interpolated frame is included.
- GitHub-compatible Markdown/HTML uses aspect-preserving images and width limits;
  the two-column gallery can scroll on narrow GitHub layouts. Static structure
  and relative links were checked. A private offline browser preview was attempted with GPU disabled, but Chrome
  could not start under the available socket restrictions. Live GitHub desktop/mobile
  rendering remains unverified; static responsive structure was checked. Main README embeds five GIFs;
  further recordings are kept in the gallery rather than expanding the landing page.

## Provenance, rights and external links

The owner explicitly confirmed first-party media/artifact approvals. Previously
published report media retains CC BY 4.0 attribution. New first-party media is not
assigned a blanket license. Exact Stage 1–3 checkpoint footage and the physical
clip's policy identity remain unresolved; the README does not invent them.

The GitHub connector successfully read the existing public report-media README.
Direct binary-video fetches were unsupported/too large, and terminal HEAD checks
could not resolve github.com. Public report/video references are retained from
the approved provenance, but current binary playback reachability is **not**
reported as independently passing. New block/terrain/hardware full-video hosting
is pending; no upload or invented URL was created.

## Disclosure boundary and Git isolation

The candidate contains only Markdown, citation/data/provenance files, selected
GIF/PNG assets, a benchmark PNG and a conceptual SVG and the scoped license text. It contains no
Python/C++/shell training code, specialized actor, reward/configuration/curriculum,
detector, deployment controller, private logs, checkpoint, export, robot asset,
submodule, symlink, remote, Git alternate or inherited engineering history.

Before commit, every staged path/content and allowed media identity is reviewed.
After commit, reachable commits and blobs are inspected, checked against the
selected presentation files and compared with private code blob identities.
The verification receipt is retained privately to avoid adding private paths or
code-rich inventories to the public showcase. A clean-tree check completes the
local handoff. Pattern scans are bounded disclosure checks, not legal guarantees.

## Reproduction and future additions

The local preparation tooling is intentionally private. It performs file hashing,
FFprobe metadata inspection, CPU excerpt conversion and asset/link/disclosure
checks without importing policy or simulator code. See
[media-updates.md](media-updates.md) for the incremental workflow and
[media-provenance.json](media-provenance.json) for the included derivative identities.

No benchmark samples were added or removed; published counts and denominators
were checked. MuJoCo R2 FAIL, V1 parity FAIL, V2 batch-1 scoped PASS and
`approved_for_actuation: false` remain explicit. No publication or next campaign
was initiated.
