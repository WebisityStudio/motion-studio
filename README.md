# Motion Studio for Claude Code

Give Claude your brand, assets and a brief. Invoke `/motion-studio` to work through visual direction, a storyboard, a moving draft, rendering and evidence-based quality checks.

This is a **Claude Code skill**, not a video model, hosted service or bundled rendering engine. It tells Claude how to run a production workflow with the tools available in your project. Rendering dependencies and any external services are separate.

## Install

Requires local Claude Code with skills support. Review the skill before installing. No install script or automatic dependency downloads are included.

### macOS / Linux

Clone this repository into a new folder:

```bash
git clone https://github.com/WebisityStudio/motion-studio.git motion-studio-skill
mkdir -p ~/.claude/skills
```

Copy the repository's **`motion-studio` subfolder** into `~/.claude/skills/`. If a skill with that name already exists, back it up or compare versions before replacing it. For a new installation:

```bash
cp -R motion-studio-skill/motion-studio ~/.claude/skills/motion-studio
```

### Windows

Clone or download this repository, then copy its `motion-studio` subfolder to `%USERPROFILE%\.claude\skills\motion-studio`.

### Project-only installation

Instead of the personal skills folder, copy the same subfolder into your project's `.claude/skills/` directory.

Start a new local Claude Code session. Test without creating a video:

```text
/motion-studio dry-run a 30-second vertical product video
```

Personal local installation does not automatically install this into Claude web chat, Cowork or cloud sessions. See [Claude Code's official skills documentation](https://code.claude.com/docs/en/skills).

## Use

```text
/motion-studio

Brand: [website or brand folder]
Assets: [local folder or attached files]
Reference: [optional image or video]

Create a polished 30-second vertical motion video.
Use our actual branding and assets.
Show me the storyboard before building.
Save the final MP4 locally. Do not publish it.
```

For end-to-end creative delegation:

```text
/motion-studio Create a 45-second landscape launch film using ./brand and ./assets.
You have creative freedom over the story, transitions and sound.
Handle the storyboard, moving draft, render, critique and fixes without a storyboard approval pause.
Use existing approved local tools only. Ask before installs or paid services.
```

Other modes:

```text
/motion-studio plan-only a product launch film using ./assets
/motion-studio dry-run a 30-second vertical brand film
/motion-studio full-journey 75s landscape, connecting verified product features
```

- **`plan-only`**: research and storyboard; no render.
- **`dry-run`**: read-only explanation; no file creation, browsers, installs or rendering.
- **Normal invocation**: discover assets, direct the film, build, critique and export.

The skill is deliberately **manually invoked**. It does not automatically start production when you mention a video.

## Production approach

1. Inspect existing work and verify assets and product claims.
2. Extract visual direction from a reference or brand.
3. Write a timestamped storyboard.
4. Reuse an appropriate renderer with deterministic frame access.
5. Review representative stills and a low-resolution moving draft.
6. Fix timestamped problems, then render requested formats.
7. Check decoding, dimensions, duration, readability, audio and full-film coverage.

Defaults: 30 seconds, vertical 1080×1920, 30 fps, local brand assets and licensed audio, no paid calls. Explicit briefs override defaults.

## Boundaries and limitations

- The skill does not include product footage, music, fonts, a renderer or paid-service credentials.
- Tool availability, model capability, compute and the brief affect results. No quality, speed or cost guarantee.
- It favours existing project tooling; it does not silently install frameworks.
- Reference images inspire visual grammar, not permission to copy protected assets.
- Product animations must not be passed off as recordings of verified working features.
- Stills cannot establish smooth motion or audio sync. Unavailable visual/audio checks must be disclosed.
- Publishing, uploading private data, paid services and destructive actions require separate approval.
- No private project presets, personal machine paths or credentials are included.

## Files

- `motion-studio/SKILL.md`: invocable workflow.
- `motion-studio/references/production-contract.md`: rendering and quality-control criteria.

## Acknowledgement

Inspired by the production workflow discussed in [Movez's motion-design article](https://x.com/0xMovez/status/2104216919033192746). This is an independently adapted workflow, not an official Anthropic tool or endorsement. The article's promotional performance and model claims are not guarantees of this skill.

## Licence

MIT. This licence covers the skill documentation in this repository, not third-party assets, software or generated media rights.
