# STORYBOARD.md — SunrAI, form B: the authored stage

Status: delivered
Date: 2026-11-15
Owner: Guillermo Villegas
Renderer: hand-authored HTML/CSS/JS (no bundler) + `playwright-core` frame stepping → ffmpeg x264
Master: 1920×1080, 30 fps, 72 s, silent with burned-in captions

**Form.** The product is rebuilt, screen by screen, as authored markup — the
same way a stageshow scene is authored — and filmed frame-exact off a virtual
clock. A drawn cursor performs the interaction. Nothing here is a screen
recording: every frame is composed, so the camera, the cursor and the timing are
exactly as designed, at the cost of being a reconstruction rather than the
product itself. The end card says so.

**Why authored at all.** With a fabricated stage there is no staging dependency,
no network variance, no half-loaded state and no account data in the frame. A
scene can hold the exact moment a value changes for as long as the copy needs.

**Deviation, recorded.** The `stageshow` skill's kit is React + Vite. D98 forbids
a bundler running on this host, and the four screens here are SunrAI-specific, so
the scenes are plain HTML/CSS/JS that follow the skill's craft rules
(one change per beat, locked camera, the cursor only where something is acted
on, `Act`-style scripted motion) without the kit's React runtime.

## Logline

Five moves that a solar contractor makes every week — filter the pipeline, close
out a phase, file a roof photo, answer a customer, work a hail event — each
shown as one action on one screen, so the tool's shape is legible in a minute.

## Brief

- **Audience:** the same stand audience as form A, seen second; also usable as an
  embedded clip on a landing page where a screen recording would be too heavy.
- **Must remember:** one action, one visible consequence, five times.
- **Constraints:** no invented feature. Every screen, label and number in frame
  exists in the product; the values are the seeded demo account's.

## Beats

Each scene is 12.8 s on the virtual clock, of which the first 0.55 s and last
0.45 s are the scene's own fade.

| t (s) | start frame | dur | scene | interaction | copy | hold |
|---:|---:|---:|---|---|---|---:|
| 0.0 | 0 | 4.4 | cold open | window settles 12 px up | — | 4.4 |
| 4.4 | 132 | 11.0 | **Pipeline** | cursor clicks the **Stage** filter, selects *Procurement*; eleven of thirteen rows leave, and the grid reports "2 of 13 projects" with a way back | "Filter the whole pipeline by where it stands." | 3.9 |
| 17.2 | 516 | 11.4 | **Phase close-out** | cursor ticks the first open task in *Installation*; its photo thumbnail appears; the phase meter advances one step | "Tick a task, attach the photo, the phase moves." | 3.9 |
| 30.0 | 900 | 11.8 | **Photos** | cursor opens a gallery tile; the lightbox shows the job, date and checklist step; it closes | "Every roof photo keeps its job, its date and its step." | 3.9 |
| 42.8 | 1284 | 11.8 | **Inbox** | cursor opens a conversation, types a two-line reply, sends it; the unread badge clears | "Customer texts land beside the job they are about." | 3.9 |
| 55.6 | 1668 | 11.8 | **Storm** | cursor clicks *Build a list of these neighborhoods*; a customer list assembles with a count | "One click turns a hail event into a canvassing list." | 3.9 |
| 67.4 | 2022 | 4.6 | end card | wordmark, one line, disclosure | "Interface recreated for film." | 4.0 |

Reading floor `max(1.0 s, 0.6 s + 0.3 s × words)`:

| copy | words | floor | allotted |
|---|---:|---:|---:|
| Filter the whole pipeline by where it stands. | 8 | 3.0 s | 10.2 s |
| Tick a task, attach the photo, the phase moves. | 9 | 3.3 s | 10.2 s |
| Every roof photo keeps its job, its date and its step. | 10 | 3.6 s | 10.2 s |
| Customer texts land beside the job they are about. | 9 | 3.3 s | 10.2 s |
| One click turns a hail event into a canvassing list. | 10 | 3.6 s | 10.2 s |

## Narration script

| in | out | line |
|---|---|---|
| 00:04.4 | 00:08.6 | Filter the whole pipeline by where it stands. |
| 00:17.2 | 00:21.4 | Tick a task, attach the photo, the phase moves. |
| 00:30.0 | 00:34.6 | Every roof photo keeps its job, its date and its step. |
| 00:42.8 | 00:47.4 | Customer texts land beside the job they are about. |
| 00:55.6 | 00:59.6 | One click turns a hail event into a canvassing list. |
| 01:04.4 | 01:08.6 | SunrAI. Interface recreated for film. |

Delivered as `videos/stage/NARRATION.srt` and `SCRIPT.md`.

## Style frames

- [ ] Opening — cold open with the window's soft edge
- [ ] Hero / reveal — the pipeline after the filter
- [ ] Proof / product — the phase meter advancing
- [ ] CTA — end card
- [ ] Logo — wordmark on `#09090B`

## Sound plan

- Music: none.
- Cues: none. Clicks are drawn, not sounded; the silent film is the deliverable
  and a voiced cut is laid over the same timecodes.
- Voice: unrecorded, as in form A (no ElevenLabs credential in this environment).
- Silence: throughout.

## Approval

- Logline / beats: drafted 2026-11-15, not yet approved.

## Review notes

| Date | Reviewer | Finding | Fix | Re-rendered |
|---|---|---|---|---|
| | | | | |

## Risks

- **Authoring divergence.** A rebuilt screen drifts from the real one as the
  product changes. Mitigation: every scene is compared frame-to-frame against
  the real capture in `videos/_capture/out/` at review, and the disclosure line
  is mandatory whenever this form is shown to a customer.
- **Claims that need evidence.** The counts drawn in the scenes are the seeded
  account's: 13 projects, 507 open tasks, 29 overdue, 5 inspections booked, 28
  photos. They were read from staging with SQL against `projects`, `tasks`
  (status not `Done`), `inspections` (status `scheduled`) and the two photo
  tables — the same queries recorded in `videos/README.md` — not typed from
  memory, and the table is re-checked against `videos/_capture/out/` at review.
- **UI that must be the real product.** None of it — which is the whole point,
  and the whole risk. This film never substitutes for a demonstration of the
  real product, and it is labelled.
- **Anything generated.** The screens are authored. No photograph in frame is
  generated; the roof photos are SunrAI's own landing assets.
