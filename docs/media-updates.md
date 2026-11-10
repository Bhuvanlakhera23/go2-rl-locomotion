# Adding existing media without rebuilding the showcase

1. Add originals to the owner's separate curated media collection. Leave existing
   originals unchanged. The collection is not part of this repository.
2. Use the private media-preparation helper to rediscover files, read metadata and
   identify duplicate SHA256 hashes. A hash match establishes duplicate bytes,
   not a policy identity or a new rights grant.
3. Record simulation/hardware classification, policy evidence, caption source and
   release scope. Keep unverified values explicit and obtain owner approval for
   future additions; this review's authorization is not automatic future approval.
4. Choose one short, informative continuous segment. Create a separate derivative
   with CPU FFmpeg: approximately 3–8 s, 10–15 fps and display-appropriate width.
   Preserve timeline speed, aspect ratio and essential scene context. Inspect it.
5. Add only the selected GIF/image, update `media-provenance.json` and link it in
   the gallery. Add to the main README only if it contributes a distinct result.
   No complete rebuild or original-video commit is required.
6. Recheck hashes, dimensions, frame timing, captions, local links and disclosure
   boundaries. Strip private paths/metadata from the public record. Full videos
   need separately selected hosting; never invent a public URL.
7. Review the staged files and independent Git history before any owner-authorized
   publication. Never add private source, weights, exported policies or assets.

The preparation helper, full absolute-path inventory and contact sheets are
private and deliberately outside this presentation-only repository. The public
manifest records stable logical source IDs and original/derived hashes instead.
