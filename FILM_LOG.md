# FILM_LOG.md — what was built, what it cost, what is not proven

Three demonstration films of SunrAI for a trade show, each a different form, all
from the same demo account. This is the record of how they were made and what is
actually verified about them.

## The one-paragraph version

Form A records the real product on staging with a real pointer and cuts the
recording to the beats with a camera that crops to whatever the pointer is doing.
Form B is an authored stage in the product's visual language, stepped from a
virtual clock, so every beat holds exactly as long as its copy needs. Form C
treats the product's own screenshots as material: camera pushes, masked reveals,
figures lifted out as type. All three are silent with captions burned in, and each
carries a narration script timed off its own cut.

## What is on screen, and where each number came from

The demo account is the staging team **Meridian Solar**
(`591845c1-b8b3-489a-be66-2f09027e63fd`), seeded by `videos/_capture/seed_demo.py`:
16 customers, 13 jobs, 117 phases, 711 tasks, 28 photos across two tables, 11
invoices with real amounts and statuses, 5 storm events with 10 matched customers,
6 appointments, 8 leads, 7 live designs.

Every figure a film states is generated, not typed:

- `videos/lib/figures.py` reads the demo team and writes `videos/lib/figures.js`.
  Both authored films import it, so a scene cannot carry a number the database
  does not have.
- Form A has no figures of its own: it is the product, so its numbers are the
  product's.
- The one number the product computes in the browser — the Tasks screen's "open
  tasks" — is read off that screen by `videos/_capture/read-counts.mjs` and
  recorded in `figures.py` as `APP_READ_OPEN_TASKS`. Rebuilding it in SQL gives a
  different number wearing the same label.

Checked against the live screens on 2026-11-15, in the account's own timezone
(Chicago): **13 projects, 228 open tasks, 14 overdue, 9 inspections, 11 invoices,
5 storm events.** The invoice page was read row by row: statuses Paid, Sent,
Partially Paid and Overdue match the table, and Amount due is $0.00 only where the
invoice is paid.

## Form A — the live product

The recording is driven by `videos/_capture/live.mjs`, which signs in with the
saved storage state, performs each interaction with the real pointer, and writes
`videos/live/beats-log.json` with a mark per beat. `videos/live/make-schedule.py`
then turns the marks into `schedule.js`, which `videos/live/film.html` seeks
frame by frame.

Three things had to be got right, and each was wrong first:

1. **A beat that reports success without a screen is a lie.** The harness used to
   mark a beat `ok` as soon as its click returned, so a lightbox left open, a menu
   that closed without navigating, or a page that painted nine seconds later all
   passed — and the film captioned the previous screen. Every navigation now
   asserts its destination: the URL *and* a marker string the page itself renders
   (`open task`, `Affected customers`, `New invoice`, a real `$1,234.00`). A beat
   that never reaches its marker fails, and `make-schedule.py` refuses to build a
   schedule from a run with a failed beat.
2. **The recording's clock is not the harness's clock.** The recorder's frame
   timestamps stretch over a still page and compress over a busy one, so a window
   computed from wall-clock marks drifts — by the end of a two-minute session it
   lands several seconds off, on the wrong screen. The windows in `make-schedule.py`
   are therefore measured off the recording itself (a contact sheet plus frames at
   the transitions), not derived from the marks.
3. **What was not captured is not in the film.** The storm page, the dispatch
   board and a photo lightbox did not survive into the recording as usable frames.
   They are dropped from form A rather than faked: form A is nine screens —
   Home, the pipeline, the job record, its phases, its task list, the photos, the
   work list, invoices, designs — and its narration says only what those screens
   say. Forms B and C carry storm.

Re-record with:

```bash
node videos/_capture/live.mjs                    # needs the demo team and the saved sign-in
cp /tmp/live-rec/<recording>.webm videos/live/src.webm
python3 videos/live/make-schedule.py             # also writes SCRIPT.md and NARRATION.srt
node videos/lib/render.mjs --url "file://$PWD/videos/live/film.html" \
  --out videos/live/out/sunrai-live-1080p.mp4
```

## Forms B and C — the authored ones

`videos/stage/film.html` and `videos/motion/film.html` are single pages stepped by
`videos/lib/render.mjs` at 30 fps. Both are authored, and both say so: B is a
second implementation of the interface, C is stills of the real product. Neither is
presented as a recording.

Their scripts are generated from their own caption tables
(`python3 videos/lib/script-from-captions.py stage motion`), so a retimed scene
cannot leave a stale timing table behind. The earlier hand-kept files said 63 and
61 seconds while the films ran 72 and 76.

## Verification performed

- `node videos/_capture/live.mjs` — 14 beats, 0 failed, record opened at
  `…/projects/550c8bd7-e3a1-58b5-99c4-dee8c1f6ad0e`.
- `node videos/_capture/probe-film.mjs <film.html> <seconds…>` — every shot of A
  checked frame by frame against the caption it carries; every shot of B and C
  spot-checked.
- `node videos/_capture/read-counts.mjs` — 228 open tasks, 9 inspections, 13
  projects read off the product.
- `node videos/_capture/page-probe.mjs 'tasks?view=overdue'` — "Showing 1–14 of 14
  overdue tasks", which is what the films say.

## Delivered

| Form | File | Length | Size |
|---|---|---:|---:|
| A — live | `sunrai-live-1080p.mp4` | 0:59 | 9.4 MB |
| B — staged | `sunrai-stage-1080p.mp4` | 1:12 | 7.3 MB |
| C — motion | `sunrai-motion-1080p.mp4` | 1:16 | 37.8 MB |

Assembled by `python3 videos/lib/build-deliverable.py` into `videos/deliverable/`
(films, scripts, subtitles, `index.html`), and published to the owner as an
Access-gated link to `~/sunrai-demo-films` — the link tool refuses a path with a
dot directory in it, so the copy sits outside `.worktrees`.

## Narration

The films are silent. The narration exists as text timed to each cut
(`SCRIPT.md`, `NARRATION.srt`), and `videos/lib/narrate.py` turns that into a
spoken track: ElevenLabs premade **Sarah** (`EXAVITQu4vr4xnSDxMaL`) on
`eleven_multilingual_v2`, one request per line, each placed at its line's `in`
time over a silent bed, loudness-normalised to −16 LUFS, and muxed with the
picture stream copied.

```bash
ELEVENLABS_API_KEY=… python3 videos/lib/narrate.py live stage motion
```

That voice and model are the ones the 2026-11-14 trade-show demos in
`~/development/sunrai-stack-reports/trade-show-demos-20261114` were narrated
with, and their audio and alignments are still in that workspace — so the token
exists and the pipeline is proven end to end against the real API.

**It is not readable from this host today.** `ELEVENLABS_API_KEY` is not in the
environment, `ao grant list --json` returns `[]`, `scripts/integration_secrets.py
status` has no ElevenLabs row, and while the VM's service account can read the
one Cloudflare link secret it needs, it gets `PERMISSION_DENIED` on
`secretmanager.versions.access` for `ELEVENLABS_API_KEY`. The earlier run had the
key exported in its own shell; this one does not.

What that leaves unproven is only the API call. The rest of the path is tested
without a credential: `narrate.py --self-test` substitutes a locally generated
tone for each line and runs the real scheduling, placement and mux.

```
live: self-test ok — 9 lines, audio 59.50s vs film 59.50s, streams ['video', 'audio']
stage: self-test ok — 5 lines, audio 72.00s vs film 72.00s, streams ['video', 'audio']
motion: self-test ok — 6 lines, audio 76.00s vs film 76.00s, streams ['video', 'audio']
```

## Where the reference material came from

- Skill: `agent-operations/skills/motion-video` (`SKILL.md` plus references on
  AI video, motion engineering, renderers, storyboard-and-review and the audited
  skill packs).
- Research and design libraries: `~/development/design-library` (dated research
  notes and `design-index`) and `agent-operations/skills/research-library`; the
  hosted portal answers, e.g. `research_hosted.py search "motion video skill
  packs elevenlabs narration"` → the 2026-11-10 motion-skill-packs and
  motion-video-generation notes.

## Not proven

- **No audio in these three films.** The narration is written, timed and one
  command from recorded; see above for exactly what is missing.
- **Nothing is promoted or published.** The films live in this worktree and in the
  delivered folder; the link is a file tunnel, not a release.
- **The design thumbnails look schematic.** The seven seeded designs render as
  the same flat green plan outline, because the seeded geometry is a single
  rectangle. The cards' figures and addresses are real; the picture is thin.
- **B is a reconstruction** of the interface, correct as of the demo data on
  2026-11-15. A UI change invalidates the parts it touches; A does not have that
  problem, which is the trade the two forms make against each other.
- **The demo data ages.** Dates are relative to the seed run, so a film made today
  says "Nov 13" where next month's seed would say something else. Re-seeding and
  re-recording is the honest refresh.
