# Rewrite Backlog

Work on `rewrite/mantine` within the requested 12-hour implementation budget. Keep the rewrite undeployed and pause for review before merging. Prioritise working, verified workflows; fixtures do not establish live generation or migration readiness.

## Current Work

- [ ] Complete the full check, build, browser and container verification after integration; commit coherent outcomes and leave the preview running.
- [ ] Profile actual interaction long tasks/frame intervals on representative GPU hardware; retain reduced-motion and shared animation-speed controls.
- [ ] Continue source and browser comparison for flow, focus, spacing and motion using the published legacy image with isolated sample data. Fresh authenticated legacy visual review remains blocked by the credential guard.
- [ ] Rebuild the worker image with non-blocking provider discovery and verify its packaged runtime. The live incident fixes for terminal progress and stale recovery are also retained in the rewrite.

## Required Before Cutover

- [ ] Exercise real Image → Refine → Animate, references, masks, upscale/comparison, video extension, LoRAs, model/preset reuse, downloads and Library imports/grading against intended workers.
      Live image generation and reference-based Fibo refinement are verified with saved results. Cloud is offline and the user has asked to omit live cloud checks for now. GPU video is offline. Browser fixtures cover the complete session workflow on desktop, phone Chromium and phone WebKit.
- [ ] Verify administrator/user isolation, Cloud Models and NSFW grants with real accounts, including OIDC and old result links.
- [ ] Rehearse migration and restoration on a protected copy of actual runtime state; report mappings/conflicts and verify media/result links and account ownership.
      A stable read-only capture of 135 live metadata files passed local dry run, SQLite apply, repeated-apply protection and byte-exact restoration: 2 accounts, 7,082 gallery records, 19 deletion markers, zero conflicts or unmatched gallery owners. All three account folders were retained. The rewrite reads all 36 profiles, their version history, 10 guide packs and 140 catalogue entries without changing their definitions. Legacy and rewrite readers also agree on 1,176 stored result links, 1,568 job owners and 1,094 result numbers, including audience restrictions and legacy sealed tokens. Retain deployment-owned `STUDIO_MODEL_MANIFEST_PREFIX` when moving the catalogue. Media bytes, HTTP result-link delivery and authenticated account behaviour still need verification.
- [ ] Verify the app and worker images, GPU lease exclusion, offline/startup failures, cancellation/retry, restart recovery and safe saved-output workload switching.
      Both images build locally; the AMD64 app passes read-only runtime, SQLite and Sharp smoke checks, and the packaged worker passes CPU-only lease/loader/bridge checks. GPU runtime switching remains fixture-verified.
- [ ] After publishing the verified worker image, update ai's workload image references and retire the old worker recipe from images together. Existing image consumers and the images checkout remain unchanged during this review.
- [ ] Confirm AI Control relinquishes runtime ownership and every managed local text caller uses Studio admission before enabling automatic control.
- [ ] Verify stream draining and independent GPU/cloud work with real services. Live authenticated Bifrost ai/text discussion completed in 9.081 seconds with 1556 characters and no media jobs. Managed Radiance stream draining still needs live verification; LiteLLM → Bifrost migration is separate.
- [ ] Review the large rewrite before merge; keep production single-replica with Recreate. Publish and deploy only through the verified image pipeline.

## Deferred Decisions & Work

- Ownership decision updated: Studio owns and edits live profiles, guides and catalogue data. ai supplies deployment configuration and seed/backup definitions; automatic synchronisation remains out of scope.
- Chat now includes text conversation and requested media generation; the user explicitly replaced the earlier general-chat deferral. Cloud remains outside live verification while offline.
- Queue pause/reordering and Kubernetes runtime control are deferred.
- Remaining legacy API/domain internals can be removed or converted to TypeScript as their replacements become verified; retain only live-data and external-contract compatibility.
- GitHub fork-network changes and other sessions' branches/worktrees remain outside this rewrite.
- The old TASKS backlog's unprovisioned additional AI Control administrator keys belong to that service, not Studio's rewrite.

- After this rewrite is merged, migrate local plaintext environment secrets to root `fnox.toml`, following `../actual-up/fnox.toml`. Use per-vault 1Password providers with vault names and item titles, never IDs or tokens: cluster vault Kubelab SYD/Studio; local-tools-only secrets use the global Automation provider. Wrap secret-consuming Mise tasks with `fnox exec --`, update README and example environment files, verify non-empty resolution with `~/.cache/rotate/fnox-nonempty.sh` (`fnox check` is insufficient), run the app and list missing items/fields without editing 1Password. Retain plaintext environment files until the user deletes them after the PR is merged and verified.
