# Rewrite Backlog

## Goal

Bring `rewrite/mantine` to clear parity with legacy Studio and beyond it in UI/UX quality, with one tidy, pattern-led codebase that stays maintainable. Done means every workstream below is checked off or explicitly deferred, `mise run check` and full browser acceptance pass on a fresh build, the preview is running and PR #61 is ready for review. Never merge or deploy; the user reviews first.

## Working Rules

- Follow `AGENTS.md` and `UI-PATTERNS.md`; its Code Structure section holds the implementation conventions. Compare behaviour against legacy (`/private/tmp/studio-legacy-60vrohc3`, sample instance `http://127.0.0.1:18990`), not just feature lists.
- Work top to bottom. Foundations (F) land before the area workstreams that depend on them. One owner per file; serialise `mise run check`, builds and full browser runs.
- One outcome per commit on `rewrite/mantine`, pushed after its focused checks pass. Rebuild `dist/` before browser runs; Playwright serves the build.
- Items marked **(Q)** wait on Questions for Max. Do not implement them, do not stop for them: continue with the next item.
- New questions go in Questions for Max with a recommendation; finished items are checked off with a short evidence note.
- Never generate media or call cloud from tests or audits; cloud is offline. Do not change live infrastructure.

## Foundations (F) — Large

Shared owners first, so area fixes reuse them instead of adding copies. Audit reports: `/private/tmp/studio-audit-reports/`.

- [ ] F1 Extract one `GenerationEditor` used by the gallery composer and timeline cards (prompt, history, assistant, input rail, references, masks, settings, footer, submit shortcut). Cards keep only their form state and submit. Restores Prompt Assistant, masks, reference guards and blocked reasons in cards.
- [ ] F2 One exported `queryOptions` per server resource beside its owner (`models`, `own-account`, `lora-info`, …); one `Account` type; `UpscaleQuality` from `shared/`.
- [ ] F3 One `useIsAdmin()` and one `usePhone()` (from theme breakpoints); replace the four admin checks and 13 media-query strings.
- [ ] F4 Shared `ConfirmDialog`, `StudioLogo` and `copyText(text, label)`; replace the hand-built copies.
- [ ] F5 Errors: failed forms render `mutation.error` inline; action failures use one `MutationCache` `onError` default. Remove per-call `onError: failure` and duplicate surfaces (generation submit, sign-in, Settings forms).
- [ ] F6 One shared item-actions list for tile menu, context menu, viewer More menu and session results, with consistent icons, order and heights.
- [ ] F7 `WorkspaceSections` renders each section's heading and description; Library and Settings navigation share one definition shape.
- [ ] F8 Move shell pieces (status action, slideout, mode tabs, header options) into `features/shell/`; `ui/` keeps primitives without feature imports; break the generation↔sessions import cycle.
- [ ] F9 Styling: co-locate single-consumer `.studio-*` rules as CSS modules, move tokens and `AppShell` styles into `theme.ts`, set shared `ActionIcon` defaults and remove per-call sizes/radii, delete CSS that repeats Mantine's baseline.

## Generation Controls (G) — Medium

- [ ] G1 Hide settings the selected profile cannot use (steps, count/variations, denoise, fps, frames, duration); show Frames or Duration, not both.
- [ ] G2 Image/Video toggle navigates between `/images` and `/video`.
- [ ] G3 Clear resets to the empty draft for the kind, dropping Refine/Animate operation, parent and preset.
- [ ] G4 Compact composer uses the shared compact `ReferencePicker` with numbered thumbnails.
- [ ] G5 One derived submit label and `blockedReason`, shown in the Generate tooltip and accessible description (focusable when blocked).
- [ ] G6 Successful submit notifies and invalidates the gallery so the pending tile appears immediately.
- [ ] G7 Profile picker shows readiness/offline state; dropdown wide enough for full names, opening downward.
- [ ] G8 Desktop LoRA/Reference popovers drop phone Back/Use actions; LoRA panel loses repeated labels and the stray `0`, gains an empty state and a selection summary on its trigger.
- [ ] G9 Size picker opens on the active mode, labels Video correctly and shows custom dimensions alongside presets.
- [ ] G10 Selected references sit beside their trigger; preset deletion confirms and notifies; phone sticky footer has a background.
- [ ] G11 Remove unreachable prompt validation; gate Allow Fallback on profiles with more than one worker.
- [ ] G12 Keyboard: Escape in the reference picker's nested Slot select or filter popovers closes only that layer; focus stays on the moved LoRA after Move Earlier/Later.
- [ ] G13 (Q) Count/Steps in the rail, fixed-seed chip, 2K/4K/Megapixels and per-run Smart Upscale, LoRA strength slider/favourites/recents.

## Gallery & Viewer (V) — Medium

- [ ] V1 In-progress tiles show progress, phase and Cancel; failed tiles show the failure; Title Case status labels.
- [ ] V2 Curated details: profile name, LoRAs, references, seed/steps/CFG/sampler, output size/file, timing, readable dates; remove the raw settings dump.
- [ ] V3 Selection: Select Failed/In Progress, Stop selected running jobs, Share on phones, Delete key, context menu acting on the selection; labelled bulk actions.
- [ ] V4 Shift+F10/ContextMenu key opens a tile's menu; tile accessible names use the short title.
- [ ] V5 Viewer prefetches neighbours and shows position (n / total).
- [ ] V6 Viewer action row fits on one line (desktop and phone) with consistent controls; close action no longer overlaps the details title; desktop details rail can be hidden.
- [ ] V7 Tile captions show title, time and profile; downloads use `outputName`; distinct Recreate icon.
- [ ] V8 Paging shows only Try Again after failure; gallery and facets poll only while work is active.
- [ ] V9 Remove unused selection helpers; consistent toolbar control sizes.
- [ ] V10 (Q) Gallery grouping and Hide Failed & Queued; Star as a primary viewer action.

## Chat (C) — Medium, plus Max's requested tweaks

- [ ] C1 Cards use F1 `GenerationEditor`; Image/Video switch in cards picks a profile.
- [ ] C2 Rename sessions via the existing PATCH route; tidy default titles from the first clause.
- [ ] C3 Session results use the F6 shared actions (Star, Delete, Upscale, context menu).
- [ ] C4 Staged Refine/Animate keeps its own input instead of overwriting the composer draft; opening a session keeps unsent composer references.
- [ ] C5 Revision submissions render as one quiet line, not a repeated prompt bubble.
- [ ] C6 One card header ("Iteration 2 · Refine of 1"); consistent action wording with the gallery; no repeated steps in metadata.
- [ ] C7 Multi-output results use a compact grid; phone card footer does not wrap badly.
- [ ] C8 Phone sessions drawer has one title; sidebar uses Title Case, times as well as dates, one noun (Chat or Session) and conversation-specific empty copy.
- [ ] C9 Fix duplicate React keys in the timeline (`chat:`/`job:` prefixes) and the missing-key warning in `SessionIteration`.
- [ ] C10 Session, chat and session-list polling stops once work is terminal and nothing streams; `useMediaAction` uses the job it already has.
- [ ] C11 (Q) Session delete, text readiness from the gateway, thread alignment with the composer, and Max's Chat tweaks.

## Shell, Queue, Library & Settings (S) — Medium

- [ ] S1 Status drawer → Settings keeps the background location.
- [ ] S2 Queue rows show progress and phase with Title Case statuses; empty Queue popover/drawer sizes to content.
- [ ] S3 About shows version, Changelog, Licence, Source and credit links.
- [ ] S4 Runtime panel shows the service state, defaults to the worst/active endpoint and labels endpoints distinctly.
- [ ] S5 Library tables: responsive filters, empty state outside the scroll container, untruncated status; shared `EmptyState` Title Case copy; remove Refresh Downloads.
- [ ] S6 Account: single-user copy, account name as `Menu.Label`, sign-in errors inline, `LoadingState` in Settings sections.
- [ ] S7 Phone overflow Theme icon; status-drawer button labelled Workers.
- [ ] S8 (Q) Restore Settings sections (Studio preferences, Maintenance, model defaults), worker Test/Refresh, navigation icons and descriptions.

## Tests & Repository (T) — Small

- [ ] T1 Split `tests/browser/workflows.spec.ts` into its topic specs, keeping only cross-feature journeys; share route mocks through `fixtures.ts`.
- [ ] T2 Add a Mise task for browser tests and use it in README; remove `dev:lan`; align `package.json` ranges; delete empty scaffold directories.
- [ ] T3 Deduplicate README/CONTRIBUTING development steps and TROUBLESHOOTING/DOCKER rollback text.
- [ ] T4 Stop writing `startImageId` in new drafts once `referenceAssets` covers every reader; keep reading it for old records.
- [ ] T5 Drop `export` from symbols used only in their own file.

## Verification & Delivery

- [ ] After each workstream: full `mise run check`, fresh build, full browser acceptance and a refreshed PR verification section.
- [ ] Profile interaction long tasks/frame intervals on representative GPU hardware; retain reduced-motion and shared animation-speed controls.
- [ ] Fresh authenticated legacy visual review remains blocked by the credential guard; use the sample instance meanwhile.

## Questions for Max

1. Chat tweaks: which changes do you want? (C11)
2. Session delete: add a store/route and Delete action? Recommended: yes, with confirmation.
3. Settings: which dropped sections return — Studio preferences (Enter to Generate, Date Headers, Shortcuts, Auto-Resize Inputs, Run Several Images As, Previews While Generating), Maintenance (Clear Failed, Export Gallery, Copy Diagnostics), model defaults? Recommended: Maintenance and the preferences still backed by behaviour.
4. Workers: manual Test/Refresh while AI Control owns lifecycle? Recommended: Refresh only.
5. Navigation icons and descriptions in Library and Settings, as legacy had? Recommended: yes.
6. Gallery grouping (runs, date moments) and Hide Failed & Queued? Recommended: Hide Failed & Queued only.
7. Star as a primary viewer action on desktop and phone? Recommended: yes.
8. Generation: Count in the rail, fixed-seed chip, 2K/4K/Megapixels, per-run Smart Upscale, LoRA strength slider/favourites/recents? Recommended: Count and seed chip now; the rest as you prefer.
9. Text status: should the `ai/text` gateway count towards text readiness when local text workloads are offline? Recommended: yes.
10. Chat thread: share the composer's centre line on desktop? Recommended: yes.
11. Is the untracked `private/todo.md` retired?

## Required Before Cutover

- [ ] Exercise real Image → Refine → Animate, references, masks, upscale/comparison, video extension, LoRAs, model/preset reuse, downloads and Library imports/grading against intended workers.
      Live image generation and reference-based Fibo refinement are verified with saved results. Cloud is offline and the user has asked to omit live cloud checks for now. GPU video is offline. Browser fixtures cover the complete session workflow on desktop, phone Chromium and phone WebKit.
- [ ] Verify administrator/user isolation, Cloud Models and NSFW grants with real accounts, including OIDC and old result links.
- [ ] Rehearse migration and restoration on a protected copy of actual runtime state; report mappings/conflicts and verify media/result links and account ownership.
      A stable read-only capture of 135 live metadata files passed local dry run, SQLite apply, repeated-apply protection and byte-exact restoration: 2 accounts, 7,082 gallery records, 19 deletion markers, zero conflicts or unmatched gallery owners. All three account folders were retained. The rewrite reads all 36 profiles, their version history, 10 guide packs and 140 catalogue entries without changing their definitions. Legacy and rewrite readers also agree on 1,176 stored result links, 1,568 job owners and 1,094 result numbers, including audience restrictions and legacy sealed tokens. Retain deployment-owned `STUDIO_MODEL_MANIFEST_PREFIX` when moving the catalogue. Media bytes, HTTP result-link delivery and authenticated account behaviour still need verification.
- [ ] Verify the app and worker images, GPU lease exclusion, offline/startup failures, cancellation/retry, restart recovery and safe saved-output workload switching.
      Both images build locally; the AMD64 app passes read-only runtime, SQLite and Sharp smoke checks. The AMD64 worker, including non-blocking provider discovery, passes 84 packaged CPU lease/loader/bridge fixtures. GPU inference and runtime switching remain unverified.
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
