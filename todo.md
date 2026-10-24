# Rewrite Backlog

## Goal

Bring `rewrite/mantine` beyond legacy Studio: a clean, Grok Imagine-like media workflow (viewer iteration hub, chip composer, Runs, compact Chat, Dream with a learned taste profile), a lean MCP, and one tidy, pattern-led codebase that stays maintainable. Done means every workstream below is checked off or explicitly deferred, `mise run check` and full browser acceptance pass on a fresh build, the preview is running and PR #61 is ready for review. Never merge or deploy; the user reviews first.

## Working Rules

- Follow `AGENTS.md` and `UI-PATTERNS.md`; its Code Structure section holds the implementation conventions. Compare behaviour against legacy (`/private/tmp/studio-legacy-60vrohc3`, sample instance `http://127.0.0.1:18990`), not just feature lists.
- Work top to bottom: Foundations (F), Redesign (R), MCP (M), Dream (D), Tests & Repository (T). One owner per file; serialise `mise run check`, builds and full browser runs.
- One outcome per commit on `rewrite/mantine`, pushed after its focused checks pass. Rebuild `dist/` before browser runs; Playwright serves the build.
- Items marked **(Q)** wait on Questions for Max. Do not implement them, do not stop for them: continue with the next item.
- New questions go in Questions for Max with a recommendation; finished items are checked off with a short evidence note.
- Never generate media or call cloud from tests or audits; cloud is offline. Do not change live infrastructure.

## Foundations (F) — Large, first

Shared owners first, so later work reuses them instead of adding copies. Audit evidence: `/private/tmp/studio-audit-reports/`.

- [ ] F1 Extract one `GenerationEditor` used by the gallery composer, viewer hub and Chat cards (prompt, history, assistant, chip rail, references, masks, settings, footer, submit shortcut). Callers keep only their state and submit.
- [ ] F2 One exported `queryOptions` per server resource beside its owner (`models`, `own-account`, `lora-info`, …); one `Account` type; `UpscaleQuality` from `shared/`.
- [ ] F3 One `useIsAdmin()` and one `usePhone()` (from theme breakpoints); replace the four admin checks and 13 media-query strings.
- [ ] F4 Shared `ConfirmDialog`, `StudioLogo` and `copyText(text, label)`; replace the hand-built copies.
- [ ] F5 Errors: failed forms render `mutation.error` inline; action failures use one `MutationCache` `onError` default. Remove per-call `onError: failure` and duplicate surfaces.
- [ ] F6 One shared item-actions list for tiles, context menus, viewer and Chat results, with consistent icons, order and heights.
- [ ] F7 `WorkspaceSections` renders each section's icon, heading and description; Library and Settings share one definition shape.
- [ ] F8 Move shell pieces into `features/shell/`; `ui/` keeps primitives without feature imports; break the generation↔sessions import cycle.
- [ ] F9 Theme: one self-contained `theme.ts` with glass surfaces throughout via theme defaults, shared `ActionIcon` sizes, tokens and `AppShell` styles; co-locate remaining single-consumer CSS as modules and delete CSS that repeats Mantine's baseline.

## Redesign (R) — Large, after F

Follow the updated `UI-PATTERNS.md`; target a clean Grok Imagine-like flow. Fold the audit fixes into each item.

- [ ] R1 Composer: prompt box with history inside it and a chip rail (Profile with readiness, Aspect, Count, References with numbered thumbnails, LoRAs with summary, Presets, Expert popover showing only settings the profile supports; Frames or Duration, not both; fixed seed visible). Image/Video navigates `/images`↔`/video`; Clear resets the operation; one submit label and blocked reason; submit notifies and shows the pending tile. Phones keep the full-height editor with roomy, easy-to-edit text.
- [ ] R2 Viewer hub: prefilled prompt bar and variation strip; Star, Download/Share, Upscale, Animate ▾ (LLM themes incl. Spicy for NSFW grants and Custom Instruction), Regenerate ▾ (new seed / Exact Repeat), Copy Prompt/Settings; curated details (profile, LoRAs, references, seed/steps, output, timing); remembered desktop sidebar (default open); phone full-bleed with swipe navigate/close/details; neighbour prefetch and position; no overlapping close.
- [ ] R3 Gallery: Grid | Runs toggle with stacked run cards that fan out in place; progress, phase and Cancel on running tiles; failed tiles; selection extras (Select Failed/In Progress, Stop, Share, Delete key, context menu on selection, labelled bulk actions); Shift+F10 menus; tile captions and short accessible names; downloads use `outputName`; Try Again-only paging; poll only while work is active.
- [ ] R4 Chat: compact cards with inline Edit (shared editor), edited submissions append at the bottom as one quiet line; Chat noun everywhere; LLM titles and Rename; Delete with unticked per-result checklist (needs store/route); staged Refine/Animate keeps its own input; multi-output grid; phone drawer title; fix duplicate keys and missing-key warning; stop polling when idle.
- [ ] R5 Library & Settings: icon navigation, heading + description, segmented views, expanding search, filters in one popover, compact rows with status badges and row menus, Title Case `EmptyState`s, responsive phone layout. Settings restores Maintenance (Clear Failed, Export Gallery, Copy Diagnostics), About (version, changelog, licence, source, credits) and preferences still backed by behaviour; Workers gains Refresh; account copy fits single-user mode; sign-in errors inline.
- [ ] R6 Shell & queue: status drawer → Settings keeps background location; queue rows show progress, phase and Title Case statuses; empty popovers size to content; runtime panel shows service state with distinct endpoint labels; overflow Theme icon.
- [ ] R7 Keyboard: Escape in the reference picker's nested layers closes only that layer; focus stays on a moved LoRA.

## MCP & Assistant (M) — Medium

The MCP tools use a lot of context and iterations often call tools wrongly. The same backend serves Chat.

- [x] M1 Measured in fixtures: instructions 1,227 chars and 9 tools at 8.4k chars are modest; the cost is in results (1024px inline preview per output plus full settings records) and confusing schemas (27 Generate parameters, limits that contradict descriptions, multi-mode Reuse). Reviewing real LibreChat traces needs a read of production chat data, which the permission guard blocked (Question 3).
- [ ] M2 Slim tool surface: fewer, clearer tools; short descriptions; compact schemas with enums/defaults; concise results that reference IDs instead of repeating inputs.
- [ ] M3 Make iteration hard to get wrong: one iterate tool taking a result ID and changes; validation errors that say the correct call; examples in descriptions only where they prevent observed mistakes.
- [ ] M4 Chat uses the same slimmed tools and taste profile; eval with `mise run eval:assistant`.

## Dream & Taste (D) — Large, after R

- [ ] D1 Taste profile: LLM-maintained, editable summary from swipes, stars, iterations, prompts and LoRAs; stored per account.
- [ ] D2 Dream scheduler: idle-only, yields to user and text work, unseen buffer and daily cap; images, videos and NSFW-granted spicy content; separate pool until kept.
- [ ] D3 `/dream` deck: swipe left discard, right keep, up keep + variations; Star and Animate buttons; pause and settings; discards retained and filterable.
- [ ] D4 Suggestions: composer prompt ideas, viewer next-step chips and Chat context from the taste profile.

## Later (L)

- [ ] L1 CivArchive (`https://civarchive.com/`) as a Library download and lookup source alongside Civitai and Hugging Face: search/resolve model and LoRA pages, catalogue metadata and downloads through the existing download queue. Check its terms and API before building.

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

1. Bring back 2K/4K/Megapixels sizing, per-run Smart Upscale and LoRA strength sliders/favourites/recents? Recommended: Megapixels in Aspect and per-run Smart Upscale in Expert; LoRA favourites later.
2. Is the untracked `private/todo.md` retired?
3. MCP traces: may I read recent Studio tool calls from LibreChat's database read-only (tool names, argument shapes and errors only, no message text printed)? It needs a permission rule for production reads, or you can export a few failing conversations. Meanwhile M2/M3 proceed from the measured causes.
4. Kubelab's LibreChat Studio `promptPrefix` repeats and partly contradicts Studio's own MCP instructions. Remove it once M2/M3 land? Recommended: yes, in a separate kubelab PR.

Settled 24 Oct: viewer hub, chip composer, Grid | Runs, compact Chat cards, Chat noun and LLM titles, unticked delete checklist, legacy-style Library/Settings, glass everywhere via one extractable theme, phone full-height editor, Dream as a fourth mode with idle-only capped generation and an LLM taste profile. Not wanted: gateway-based text readiness, centring the thread on the composer.

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
