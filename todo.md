# Rewrite Backlog

Work on `rewrite/mantine` within the requested 12-hour implementation budget. Keep the live application unchanged and pause for review before merging. Prioritise working, verified workflows; fixtures do not establish live generation or migration readiness.

## Current Work

- [x] Branch from current main, preserve existing work and remove the obsolete upstream remote.
- [x] Replace the legacy frontend with React, Mantine, declarative React Router and TanStack Query.
- [x] Use Chat, Images and Videos tabs (Images landing); keep the gallery composer at the bottom, expanding upwards; present media iterations with side sessions in Chat.
- [x] Group models Family → Model or Finetune → Fast/Quality or workflow preset. Group LoRAs Family → Type.
- [x] Keep Layout within the header theme popover; order Animations, Background, Colour, Colour Scheme, Corners and Layout. Follow System by default and persist preferences. Settings has no duplicate Appearance section.
- [x] Make the resting composer compact: any click inside expands it and clicking outside collapses it. Reference opens a gallery/upload picker, and gallery items can be dragged into the composer as references.
- [x] Open Library and Settings as modal workspaces, use blurred backdrops and transitions for modals, and restore a full-screen media viewer.
- [x] Add conversational Chat with streamed assistant text, automatic generation when requested, and a new editable generation-input card followed by results for each timeline iteration. Keep Images Gallery as the landing page.
- [x] Add owner-scoped SQLite sessions, queue and user presets; retain published generation validation and idempotency.
- [x] Preserve selected backend IDs, recover recorded jobs without scanning shared history, and hold workload admission through durable output saving.
- [x] Package media/text worker modes, fixed GPU leases, Docker admission and direct authenticated text-stream admission. Lifecycle control remains disabled.
- [x] Read mounted ai profiles, guides and catalogue definitions without applying stale runtime edits; keep user presets editable.
- [x] Add an offline SQLite metadata dry run, verified backup and restoration rehearsal, preserving identifiers and result links.
- [x] Consolidate application checks/build/browser/image/release workflow and separate worker publication by native path filters.
- [x] Remove the old UI, obsolete assets/dependencies, handwritten declaration companions, completed TASKS history and redundant development/release setup.
- [x] Complete direct CLIProxyAPI media generation independent of the ComfyUI GPU worker, including provider recovery and output saving; HTTP fixtures cover actual account permissions and PNG metadata reuse.
- [x] Replace loopback HTTP for core MCP generation/status/result lookup with shared in-process domain calls; retain published tool contracts.
- [x] Verify desktop/phone browser acceptance for the initial fluid gallery and iterative Chat layout: 51 Chromium/WebKit scenarios passed. Recheck the newest interaction requirements below before claiming final acceptance.
- [ ] Complete the full check, build, browser and container verification after integration; commit coherent outcomes and leave the preview running.
- [x] Move retained upscales into the durable queue, including recovery of recorded provider IDs and saving before admission release. A real 1024 → 2048 upscale saved and downloaded successfully.
- [x] Support cold startup with all workers offline: expose configured logical profiles, accept owned work and wait for the selected worker without substituting models.

## Current Interaction Checkpoint

- [x] Verify the clean Chat composer (text, references, actual assistant model selector), inline media settings, and LLM-aware revisions retaining original cards and result lineage.
- [x] Verify full-height structural sessions sidebar, Full/Fixed workspace sizing, and a centred composer capped at the shared gallery composer width in both modes.
- [x] Verify mobile header: contextual left status, centred Chat/Images/Videos icons, and one right menu ordered Account, Library, Settings, Theme, account name and Sign Out. Confirm the Theme popover anchors below the header at 320px.
- [x] Verify compact single-row gallery composer, thumbnail-only references, icon Generate when collapsed, text and icon when expanded, click-in/out behaviour and fast upward phone Drawer.
- [x] Verify shared Mantine workspace navigation, compact header section selection on phones, dense tables, authentication layout and subdued empty states.
- [x] Verify account menu name, Account and supported Sign Out; display-name updates must be reflected without duplicate Settings actions.
- [x] Verify compact active queue rows, reasons, individual Cancel/Retry and owner-scoped Cancel All. Completed work stays in Gallery/Sessions and leaves the active list.
- [x] Verify full-width expandable Gallery search, preserved query/focus and icon-triggered scrollable filter popovers; remove duplicate toolbar Queue access.
- [x] Finish the transparent fullscreen viewer with Fit → Fill → Actual Size, image wheel/pinch zoom and pan, drag-safe click cycling, native video controls and swipe/keyboard-expandable bottom details/actions.
- [x] Inspect responsive conversation screenshots and measure a reference baseline: Headless Chromium 156 at 1440px yielded 180 idle frames, median/p95 16.7ms and maximum 16.8ms. This is a 60Hz headless baseline, not proof of 120Hz interaction. Widths 320/390/768/1440/1920 had no horizontal document overflow. Transition sampling found and verified fixes for a 2px gallery search shift and incorrect first-open profile fields; no horizontal overlay overflow was observed.
- [ ] Profile actual interaction long tasks/frame intervals on representative GPU hardware; retain reduced-motion and shared animation-speed controls.
- [ ] Consolidate the duplicated generation expert fields in Gallery and Chat cards into canonical GenerationSettingsFields, preserving profile constraints; root owns this after the repository reorganisation.

## Required Before Cutover

- [ ] Exercise real Image → Refine → Animate, references, masks, upscale/comparison, video extension, LoRAs, model/preset reuse, downloads and Library imports/grading against intended workers.
      Live image generation and reference-based Fibo refinement are verified with saved results. Cloud is offline and the user has asked to omit live cloud checks for now. GPU video is offline. Browser fixtures cover the complete session workflow on desktop, phone Chromium and phone WebKit.
- [ ] Verify administrator/user isolation, Cloud Models and NSFW grants with real accounts, including OIDC and old result links.
- [ ] Reconcile current live profile, guide and catalogue edits into ai before enabling mounted read-only definitions there. Do not overwrite live content from the seed.
- [ ] Rehearse migration and restoration on a protected copy of actual runtime state; report mappings/conflicts and verify media/result links and account ownership.
- [ ] Verify the app and worker images, GPU lease exclusion, offline/startup failures, cancellation/retry, restart recovery and safe saved-output workload switching.
      Both images build locally; the AMD64 app passes read-only runtime, SQLite and Sharp smoke checks, and the packaged worker passes CPU-only lease/loader/bridge checks. GPU runtime switching remains fixture-verified.
- [ ] After publishing the verified worker image, update ai's workload image references and retire the old worker recipe from images together. Existing image consumers and the images checkout remain unchanged during this review.
- [ ] Confirm AI Control relinquishes runtime ownership and every managed local text caller uses Studio admission before enabling automatic control.
- [ ] Verify stream draining and independent GPU/cloud work with real services. Live authenticated Bifrost ai/text discussion completed in 9.081 seconds with 1556 characters and no media jobs. Managed Radiance stream draining still needs live verification; LiteLLM → Bifrost migration is separate.
- [ ] Review the large rewrite before merge; keep production single-replica with Recreate. Publish and deploy only through the verified image pipeline.

## Deferred Decisions & Work

- In-app editing, draft approval and synchronisation of ai definitions remain deferred. Library file imports must not edit mounted definitions.
- Chat now includes text conversation and requested media generation; the user explicitly replaced the earlier general-chat deferral. Cloud remains outside live verification while offline.
- Queue pause/reordering and Kubernetes runtime control are deferred.
- Remaining legacy API/domain internals can be removed or converted to TypeScript as their replacements become verified; retain only live-data and external-contract compatibility.
- GitHub fork-network changes and other sessions' branches/worktrees remain outside this rewrite.
- The old TASKS backlog's unprovisioned additional AI Control administrator keys belong to that service, not Studio's rewrite.

- After this rewrite is merged, migrate local plaintext environment secrets to root `fnox.toml`, following `../actual-up/fnox.toml`. Use per-vault 1Password providers with vault names and item titles, never IDs or tokens: cluster vault Kubelab SYD/Studio; local-tools-only secrets use the global Automation provider. Wrap secret-consuming Mise tasks with `fnox exec --`, update README and example environment files, verify non-empty resolution with `~/.cache/rotate/fnox-nonempty.sh` (`fnox check` is insufficient), run the app and list missing items/fields without editing 1Password. Retain plaintext environment files until the user deletes them after the PR is merged and verified.
