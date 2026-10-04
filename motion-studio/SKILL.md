---
name: motion-studio
description: "Create reference-led motion films, product demos, launch videos and showreels. Use for motion design, animated explainers, feature clips or a connected product journey."
argument-hint: "[brief | plan-only | dry-run] [product] [duration] [formats] [reference]"
disable-model-invocation: true
user-invocable: true
---

# Motion Studio

Turn a brief into an editable, rendered, critically reviewed film. A polished animation is not proof that the product works. Preserve actual product behaviour and the provenance of every asset and claim.

## Invocation and scope

User brief: $ARGUMENTS

- `/motion-studio Acme 30s vertical` starts a product film.
- `/motion-studio Acme full-journey 75s landscape` connects verified features into one business story.
- `/motion-studio plan-only <brief>` researches local assets and writes a storyboard, but does not render.
- `/motion-studio dry-run <brief>` is strictly read-only: load this skill and its references, explain the proposed workflow, defaults, gates and missing inputs. Do not create files, open browsers, install dependencies, call paid services or render.
- No arguments: infer the product from the current project and conversation. Ask one focused question only if the subject or a consequential choice remains unclear.

Use the active model; do not change model/provider or invent effort flags. Skill invocation is not approval to publish, buy services, upload private material, change production or install third-party executables. No Git commits/pushes without permission.

## 1. Discover before building

1. Read project rules and inspect existing video sources, footage, branding and renderer before creating another pipeline. Preserve previous versions and unfinished work. Work inside the real project at `creative/motion-studio/<film-slug>/`, unless an existing production folder is specified. Never build valuable work only in temporary storage.
2. Record the brief: purpose, viewer, story, duration, aspect ratios, references, source assets, sound/voice, CTA and any approved external-service budget. Explicit user constraints override defaults.
3. Defaults when unspecified: short product film, 30 seconds, 1080x1920, 30 fps; use brand assets and existing licensed audio, no paid calls. No reference? Derive a restrained direction from the brand and label it as an assumption. Never block on optional inputs.
4. Build an asset/claim manifest: file or source URL, provenance/licence, whether real footage or staged animation, and evidence for depicted functionality. Use sanitized demo data, never private customer data. Marketing text alone does not establish a working feature.
5. Respect the user's browser and session preferences. Do not reuse authenticated sessions or switch browser profiles without approval. Establish the approved local rendering path before launching a headless browser. Prefer existing approved renderers; ask if required tools or installs are blocked. Never automate permission/password/payment UI.

Exit: scope and assets known; blockers explicit. Read [production-contract.md](references/production-contract.md) for rendering/QC.

## 2. Direct the film

1. Study the supplied visual references using actual images/video frames. Extract palette, type, composition, camera language, shot lengths and transitions into `docs/style-guide.md`. Borrow visual grammar, not copyrighted characters, logos, music or distinctive scenes.
2. Write `docs/shotlist.md`: timestamp range, visible action, exact text, asset, feature evidence, camera/motion, audio cue and transition. Keep one clear idea per shot. New visual information should serve comprehension, not a mechanical effect quota.
3. Prefer problem → real product action → visible result → outcome/CTA. For series, define shared typography, spacing, sound and transitions before splitting work.
4. Show the storyboard and assumptions. For an open-ended creative brief, wait for approval before the full build unless the user explicitly delegates end-to-end creative decisions. Silence is never approval. `plan-only` ends here.

Exit: a coherent, approved or explicitly delegated story, with no unsupported product claims.

## 3. Build a reusable timeline

- Reuse the project's engine when suitable. A small bespoke film can use a pure `seek(t)`/`draw(t)` renderer; recurring React/data-driven series can use an existing Remotion setup; existing HTML/GSAP productions can keep their engine. Do not install several frameworks just to follow a tutorial.
- Rendering must support arbitrary frame order with identical results: no state carried between frames, wall-clock timing, unseeded randomness or live network dependencies. Freeze assets and fonts. Use analytic springs or deterministic framework primitives.
- Animate authentic UI crops/components, with legible focus and context. Distinguish a staged UI sequence from a live recording. Do not invent clicks, responses or functionality and pass them off as a real demonstration.
- Give motion weight and hierarchy without excessive bounce, gratuitous particles, generic gradient/title sequences or unreadable rapid swaps. Design first and last frames intentionally; loop only when the brief calls for it.
- Treat each requested aspect ratio as a layout variant on one timeline, not a blind crop.
- Build representative stills and a low-resolution moving animatic before final polish. Resolve story/readability/pacing issues before expensive rendering.

## 4. Sound and critique loop

- Use supplied music unchanged if requested and rights allow it. Measure beats; manually verify the musical downbeat instead of labelling every fourth detected beat a downbeat. Do not force every action onto the beat.
- Use original synthesized sound or licensed local assets if appropriate. Avoid turning every transition into a whoosh. Narration describes the visible action at that time. Honour the requested voice and provider; never silently substitute them.
- Read credentials only through approved secret sources at runtime; never put values in prompts, files or logs. External voice/video/image calls need approved data-sharing and spend scope.
- Critique actual outputs, not source code. Inspect full-duration contact sheets, phone-sized frames, moving transition clips and audio where the tools support listening. Stills cannot verify smooth motion or sound sync. Disclose untested sensory checks.
- Log timestamped defects, severity, remedy and verification in `docs/review-log.md`. Fix the worst problems and re-render affected shots. Do at least one revision and re-check pass where defects exist; do not manufacture fixes if it already passes. Bound iterations (normally three rounds), then report unresolved blockers rather than looping indefinitely.
- Self-scores are advisory, not a pass condition. Missing assets, unsupported claims, clipped/unreadable copy, broken transitions or missing required audio block delivery as final.

## 5. Verify and deliver

Follow the concrete checks in [production-contract.md](references/production-contract.md). Verify every requested format, not just the first. Keep sources, timeline, assets manifest, reproducible commands and tool versions with the project.

Deliver `out/final-<format>.mp4`, poster, full-duration contact sheets, `docs/review-log.md` and `docs/reproduce.md`. Label incomplete work DRAFT with exact remaining issues. Report paths, dimensions, duration, audio status, checks performed and any unverified claims. Do not claim a successful render based only on files existing or an agent saying it finished. Do not publish or upload.

## Recovery

- Missing real UI: use approved existing footage or stop that shot; never substitute invented screens silently.
- Tool/credential failure: name the blocker, preserve outputs and use only approved alternatives.
- Heavy render: finish a short representative proof first, estimate from measured performance and obtain approval if it exceeds the agreed budget.
- Long session: save current scene status, asset paths, render commands and outstanding issues in `docs/checkpoint.md` for continuity.

## Source context

Adapted from the workflow discussed at https://x.com/0xMovez/status/2104216919033192746. The article's model claims, view counts, costs and install commands are not validated requirements. This skill is a production procedure, not a preinstalled render engine.
