# Rewrite Backlog

Work on `rewrite/mantine` within the requested 12-hour implementation budget. Keep the live application unchanged and pause for review before merging. Prioritise working, verified workflows; fixtures do not establish live generation or migration readiness.

## Current Work

- [x] Branch from current main, preserve existing work and remove the obsolete upstream remote.
- [x] Replace the legacy frontend with React, Mantine, declarative React Router and TanStack Query.
- [x] Use Image, Video and Chat tabs; keep the gallery composer at the bottom, expanding upwards; present media iterations with side sessions in Chat.
- [x] Group models Family → Model or Finetune → Fast/Quality or workflow preset. Group LoRAs Family → Type.
- [x] Add owner-scoped SQLite sessions, queue and user presets; retain published generation validation and idempotency.
- [x] Preserve selected backend IDs, recover recorded jobs without scanning shared history, and hold workload admission through durable output saving.
- [x] Package media/text worker modes, fixed GPU leases, Docker admission and direct authenticated text-stream admission. Lifecycle control remains disabled.
- [x] Read mounted ai profiles, guides and catalogue definitions without applying stale runtime edits; keep user presets editable.
- [x] Add an offline SQLite metadata dry run, verified backup and restoration rehearsal, preserving identifiers and result links.
- [x] Consolidate application checks/build/browser/image/release workflow and separate worker publication by native path filters.
- [x] Remove the old UI, obsolete assets/dependencies, handwritten declaration companions, completed TASKS history and redundant development/release setup.
- [x] Complete direct CLIProxyAPI media generation independent of the ComfyUI GPU worker, including provider recovery and output saving; HTTP fixtures cover actual account permissions and PNG metadata reuse.
- [x] Replace loopback HTTP for core MCP generation/status/result lookup with shared in-process domain calls; retain published tool contracts.
- [ ] Finish desktop/phone visual review and browser acceptance for the clarified fluid gallery and iterative Chat layout.
- [ ] Complete the full check, build, browser and container verification after integration; commit coherent outcomes and leave the preview running.
- [ ] Move retained upscales into the durable queue, including recovery of recorded provider IDs and saving before admission release.

## Required Before Cutover

- [ ] Exercise real Image → Refine → Animate, references, masks, upscale/comparison, video extension, LoRAs, model/preset reuse, downloads and Library imports/grading against intended workers.
      Live image generation and reference-based Fibo refinement are verified with saved results. Cloud is offline and the user has asked to omit live cloud checks for now. GPU video is offline. Browser fixtures cover the complete session workflow on desktop, phone Chromium and phone WebKit.
- [ ] Verify administrator/user isolation, Cloud Models and NSFW grants with real accounts, including OIDC and old result links.
- [ ] Reconcile current live profile, guide and catalogue edits into ai before enabling mounted read-only definitions there. Do not overwrite live content from the seed.
- [ ] Rehearse migration and restoration on a protected copy of actual runtime state; report mappings/conflicts and verify media/result links and account ownership.
- [ ] Verify the app and worker images, GPU lease exclusion, offline/startup failures, cancellation/retry, restart recovery and safe saved-output workload switching.
- [ ] Confirm AI Control relinquishes runtime ownership and every managed local text caller uses Studio admission before enabling automatic control.
- [ ] Verify stream draining and independent GPU/cloud work with real services. Bifrost-compatible fixtures do not replace live gateway verification; LiteLLM → Bifrost migration is separate.
- [ ] Review the large rewrite before merge; keep production single-replica with Recreate. Publish and deploy only through the verified image pipeline.

## Deferred Decisions & Work

- In-app editing, draft approval and synchronisation of ai definitions remain deferred. Library file imports must not edit mounted definitions.
- General conversational text chat remains deferred unless requested; Chat currently means media-focused iterative generation with inputs and sessions.
- Queue pause/reordering and Kubernetes runtime control are deferred.
- Remaining legacy API/domain internals can be removed or converted to TypeScript as their replacements become verified; retain only live-data and external-contract compatibility.
- GitHub fork-network changes and other sessions' branches/worktrees remain outside this rewrite.
- The old TASKS backlog's unprovisioned additional AI Control administrator keys belong to that service, not Studio's rewrite.
