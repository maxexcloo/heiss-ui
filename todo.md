# HEISS UI Work

## Delivery

- [x] Finish the work locally on `rebase/v0.18.0`.
- [x] Keep `main`, remote branches and the live instance unchanged. Do not push or deploy; live testing is in progress.
- [x] Preserve the original history on `backup/pre-v0.18.0-rebase-20261018`.

## Image Viewer

- [x] Open images at their native size: one image pixel per CSS pixel (1:1).
- [x] Show Zoom In, Zoom Out, 1:1 and Fit Whole Image controls on desktop and phone.
- [x] Fit the whole image inside the available viewer area without cropping or warping; preserve its aspect ratio.
- [x] Keep panning, pointer gestures, touch gestures and keyboard controls consistent with the displayed zoom.
- [x] Verify small, large, portrait and landscape images; check navigation and upscaled-output handling.

## Resolution Controls

- [x] Show resolution choices only where the selected model declares supported native output resolutions.
- [x] Include every declared supported native resolution; exclude speculative or unsupported sizes.
- [x] Use direct selection for up to two choices and a dropdown for more than two.
- [x] Keep custom dimensions and aspect-ratio controls available independently of native resolution support.
- [x] Apply the same behaviour on desktop and phone, preserving model-specific video resolution choices.
- [x] Verify submitted dimensions, model changes, saved preferences and native decoding, including 4K where supported.

## Upstream v0.18.0 Integration

- [x] Replay all 113 fork commits onto upstream v0.18.0 on an isolated branch.
- [x] Integrate native sizing, guided model setup and Edit/Reference controls with the fork's composer, gallery, workflows and LoRAs.
- [x] Preserve separate image/video backends and extend busy-state handling to each backend independently.
- [x] Port native resolution metadata, tiled large-image decoding and explicit Edit/Reference selection to MCP.
- [x] Preserve compatibility between imported and built-in FLUX.3 Klein LoRA family identifiers.
- [x] Restore the fork's unreleased changelog entries separately from upstream release notes.
- [x] Pass `mise run check`: 756 tests on the final implementation.
- [x] Build all three release archives and smoke-test the macOS packaged launcher without system Node.
- [x] Verify native 2K, Edit/Reference framing, model changes and reference replacement on desktop and phone.
- [x] Verify the phone inpainting button layout correction; the final full browser suite passes 182 tests with 24 intentional skips.
- [x] Rebuild and verify the final implementation: project checks pass, the full browser suite passes, and the final resolution-control rerun passes all 6 cases.
- [x] Refresh and smoke-test release archives after the final changes. Windows/Linux launcher execution and actual GPU generation remain unverified locally.
- [x] Review the final diff and status, run `git diff --check`, and commit the remaining local changes.

## Local Preview

- [x] Start an isolated mock preview at <http://127.0.0.1:8791> with ComfyUI discovery disabled.
- [x] Refresh and verify the preview after the final UI changes.
