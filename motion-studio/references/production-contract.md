# Production contract and verification

## Renderer acceptance

Before a full film, render a representative short shot with actual fonts/assets. Check that fonts have loaded and assets decoded, dimensions match the brief, subprocess failures propagate, ffmpeg exits zero, and the result decodes. No UI browser fallback without approval.

The scene is a pure function of time and layout. Verify at least three representative timestamps (including a transition) in sequential and shuffled order; compare decoded frame pixels or hashes of canonical raw pixels. Repeating an MP4 file hash is not a reliable frame-determinism test because container metadata may differ.

For springs: use a tested primitive or correct analytic solution. A critical-damping formula is not an exact overdamped solution. Sum step responses only for a compatible linear system, and test boundaries and text/container timing. Seeded random generators must be reset or keyed by scene/index so random access gives identical output.

If motion blur is needed, render multiple subframes at documented shutter times. Verify sample grouping, boundary handling and final frame count. Do not add expensive supersampling before the visual design passes.

## Asset and shot records

`docs/assets.md`: local path, source URL/path, rights/permission, sanitization, dimensions, and real capture vs staged animation.

`docs/shotlist.md`: time range, purpose, exact copy, visible action, asset IDs, feature evidence, camera/motion, audio cue, format-specific changes.

`docs/review-log.md`: version, timestamp, defect, severity, remedy, checked artifact and result. Label checks as automated, visually inspected, audibly inspected or unverified. Do not substitute numeric self-ratings for evidence.

## Export inspection

Default delivery: H.264, yuv420p, even dimensions, AAC when audio is required, fast-start MP4. Use the requested frame rate; 60 fps is optional, not a quality guarantee. Target roughly -14 LUFS for suitable social mixes, with true peak at or below -1 dBTP, unless a platform/brief requires another target. Measure the actual exported mix and document deviation rather than merely stating a target.

Run for each export, substituting its exact path:

```bash
ffprobe -v error -show_entries stream=codec_name,codec_type,width,height,pix_fmt,r_frame_rate,duration:format=duration,size -of json out/final-vertical.mp4
ffmpeg -v error -i out/final-vertical.mp4 -f null -
ffmpeg -hide_banner -i out/final-vertical.mp4 -af ebur128=peak=true -f null -
```

The loudness command requires an audio stream. When silence was requested, record audio as intentionally absent instead. Probe findings must match the brief, including duration, dimensions, video/audio stream presence and frame rate. Check audio end timing rather than trusting container duration alone.

Create contact sheets covering the ENTIRE film, not just the first tile page. For example this command writes successive 30-thumbnail pages rather than using `-frames:v 1`, which would stop after the first page:

```bash
ffmpeg -i out/final-vertical.mp4 -vf "fps=2,scale=270:-1,tile=6x5" -fps_mode vfr out/contact-%03d.png
```

Check the last page reaches the end and separately inspect the first and final frames. Tune sample rate and tile size to the film; fixed-rate samples can miss brief glitches.

For a suspicious transition, export a moving clip spanning both sides and inspect consecutive frames:

```bash
ffmpeg -ss 4.0 -i out/final-vertical.mp4 -t 1.0 -an -c:v libx264 -pix_fmt yuv420p out/transition-check.mp4
```

Inspect phone-width frames for text readability, overlaps, cropping, safe areas, real UI fidelity and CTA. Play/review moving sequences for stutter, abrupt cuts, timing and blur. Inspect/listen to the actual exported audio for clipping, intelligibility and cue alignment. If the available tools cannot listen or play motion, disclose that limitation and request human playback review before claiming those checks passed.

Black/silence detection is diagnostic only: deliberate fades and sparse narration can be valid. Review flags in context. For loops, check end-to-start position and velocity continuity plus audio seam, not just matching two stills.

## Pass criteria

- Every requested format exists, probes correctly and decodes without errors.
- All shots use approved/sanitized assets and evidence-backed product claims.
- Text/CTA are legible at intended viewing size, with no accidental overlap or clipping.
- No unexplained missing/black frames, broken assets, audible clipping or absent required audio.
- Motion and sound checks have explicit evidence or are clearly marked unverified.
- Final output is rechecked after fixes; previous checks do not certify a new export.
- Reproduction notes specify source location, dependency versions, exact commands, output paths and environment variable NAMES only.
