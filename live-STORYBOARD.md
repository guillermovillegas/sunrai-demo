# STORYBOARD.md — SunrAI, form A: the live product

Status: delivered
Date: 2026-11-15
Owner: Guillermo Villegas
Renderer: Playwright `recordVideo` at 1920×1080, cut frame by frame in an HTML camera page on a virtual clock, encoded with ffmpeg x264
Master: `videos/live/out/sunrai-live-1080p.mp4` — 1920×1080, 30 fps, 59.5 s, silent with burned-in captions

**Form.** A person drives the real staging product while it is being recorded.
Nothing is redrawn, mocked or re-timed: every pixel in the frame is SunrAI
serving a request, and every click is a real click the app answered. The only
post-production is a camera that crops into the recording and a caption plate.

## Logline

A solar contractor's whole week — thirteen jobs, the phases and dependencies
inside one of them, the roof photos that prove the work, the paperwork and the
hail that just hit two of their neighbourhoods — filmed as one continuous
session in the product they actually use.

## Brief

- **Audience:** a contractor evaluating SunrAI at a trade-show stand, or on a
  screen-share call. They already run a solar business and know the vocabulary.
- **Where it plays:** a 55-inch stand monitor on mute, looping; and as a link in
  a follow-up email.
- **Must remember:** the job record is one page — phase, tasks, dependencies,
  photos, permits, inspections and money all hang off it.
- **CTA:** none on screen. The end card carries the URL.
- **Constraints:** the account is `Meridian Solar` on staging, seeded for this
  film. No production data; every address, name and photograph is fictional or
  licensed for this use.

## Beats

Camera `crop` is `[x, y, w, h]` in pixels of the 1920×1080 recording. Every crop
is 16:9 and is scaled to fill the master.

The windows are **measured off the recording**, not derived from the harness's
wall-clock marks. The recorder's frame timestamps stretch over a still page and
compress over a busy one, so a mark-based window drifts — by the end of the
session it lands seconds away, on the previous screen. Each row below was read
from a contact sheet plus frames at the transition. `src` is where the shot
begins in the recording.

| t (s) | start frame | dur | beat (real interaction) | on-screen copy | camera |
|---|---|---|---|---|---|
| 0.0 | 0 | 6.0 | Home · `home` | “Thirteen jobs are running. Home says what needs you today.” | `[120, 135, 1680, 945]` |
| 6.0 | 180 | 5.0 | Pipeline · `projects` | “Every job, its stage, and the day it is next due.” | `[0, 0, 1920, 1080]` |
| 11.0 | 330 | 5.0 | The job · `open-project` | “The whole job on one page.” | `[0, 0, 1760, 990]` |
| 16.0 | 480 | 5.0 | The job · `phase-rail` | “Planning, permitting and procurement are complete. Installation is live.” | `[113, 167, 1553, 874]` |
| 21.0 | 630 | 6.0 | The job · `work-scroll` | “Each task names its owner, its due date, and what has to finish first.” | `[133, 113, 1600, 900]` |
| 27.0 | 810 | 6.0 | Photos · `photos` | “Every roof photo, filed against the job it belongs to.” | `[0, 0, 1920, 1080]` |
| 33.0 | 990 | 6.0 | Work list · `tasks` | “Overdue first, then everything else in the order it falls due.” | `[200, 80, 1520, 855]` |
| 39.0 | 1170 | 5.5 | Money · `invoices` | “Deposits, progress payments and balances, on the job they bill.” | `[0, 0, 1920, 1080]` |
| 44.5 | 1335 | 7.0 | Designs · `designs` | “Seven roof designs, each with its panel layout drawn.” | `[113, 87, 1553, 874]` |
| 51.5 | 1545 | 8.0 | end card | wordmark, one line, hold | — |

Reading floor `max(1.0 s, 0.6 s + 0.3 s × words)`, against the time each line is
actually on screen:

| copy | words | floor | allotted |
|---|---:|---:|---:|
| Thirteen jobs are running. Home says what needs you today. | 10 | 3.6 s | 6.0 s |
| Every job, its stage, and the day it is next due. | 11 | 3.9 s | 5.0 s |
| The whole job on one page. | 6 | 2.4 s | 5.0 s |
| Planning, permitting and procurement are complete. Installation is live. | 9 | 3.3 s | 5.0 s |
| Each task names its owner, its due date, and what has to finish first. | 14 | 4.8 s | 6.0 s |
| Every roof photo, filed against the job it belongs to. | 10 | 3.6 s | 6.0 s |
| Overdue first, then everything else in the order it falls due. | 11 | 3.9 s | 6.0 s |
| Deposits, progress payments and balances, on the job they bill. | 10 | 3.6 s | 5.5 s |
| Seven roof designs, each with its panel layout drawn. | 9 | 3.3 s | 7.0 s |

## What the film does not show

Four storyboarded beats have no usable footage in this recording and are cut
rather than rebuilt: the storm page, the dispatch board, the photo lightbox, and
the storm canvassing action. The recorder compressed each of those moments past
the point where a frame lands on the screen it was meant to show, and the page
markers proved the pages rendered — so the fault is in the capture, not the
product. Forms B and C carry storm. The nine shots here are the ones whose
footage was verified frame by frame.

## Narration script

Silent film with burned-in captions; this is the read that goes over it, also
written as `NARRATION.srt`. Both files are generated by
`videos/live/make-schedule.py` from the cut itself, so the timecodes cannot
drift from the picture.

| in | out | line |
|---|---|---|
| 00:00:00,200 | 00:00:05,900 | Meridian Solar, on a Thursday: thirteen jobs in flight. | 9 |
| 00:00:06,200 | 00:00:10,900 | The pipeline as one table: the stage, the next due date, the owner. | 13 |
| 00:00:11,200 | 00:00:15,900 | Open a job and the whole of it is on one page. | 12 |
| 00:00:16,200 | 00:00:20,900 | Permitting and procurement are closed. Installation is the live phase. | 10 |
| 00:00:21,200 | 00:00:26,900 | Every task names an owner, a date, and what it waits on. | 12 |
| 00:00:27,200 | 00:00:32,900 | The photographs are filed against the job, not left on a phone. | 12 |
| 00:00:33,200 | 00:00:38,900 | Then the company work list: overdue first, then everything else. | 10 |
| 00:00:39,200 | 00:00:44,400 | Deposits, progress payments and balances sit on the job they bill. | 11 |
| 00:00:44,700 | 00:00:51,400 | And the panel layout lives here too, ready to send. | 10 |

Reading rate: 99 words over 59.5 s — 100 words per minute, which is unhurried.

## Style frames

- [x] Opening — `videos/_capture/out/s-home.png`
- [x] Hero / reveal — `videos/live/poster.jpg` (the job record, "The whole job on one page.")
- [x] Proof / product — `videos/_capture/out/s-photos.png`
- [x] CTA — `videos/live/poster.jpg`, shipped as `poster-live.jpg` in the delivered folder
- [x] Logo — end card

## Sound plan

- Music: none.
- Cues: none. The film is silent by design (see `MOTION_DESIGN.md`, Sound).
- Voice: the table above, unrecorded. There is no ElevenLabs credential on this
  host: `ao grant list` reports no active grants and no `ELEVENLABS` variable is
  set. The `motion-video` skill's audited pack list rates the ElevenLabs skills
  adopt-worthy (MIT prompts over a paid hosted API), so the work is one key away
  rather than blocked on anything else.
- Silence: throughout.

## Approval

- Logline / beats: drafted 2026-11-15 from the delivered cut.
- Style frames: produced from the real capture.
- Note: "approved" is the owner's call, not an agent's. This line records that the
  film is built and verified, not that it has been signed off for a booth.

## Review notes

| Date | Reviewer | Finding | Fix | Re-rendered |
|---|---|---|---|---|
| 2026-11-15 | self | Project rows showed `—` in "Next due" on every row | seeded `projects.end_date` | yes |
| 2026-11-15 | self | Tasks screen read "No tasks yet" although 627 phase tasks existed | seeded 26 general tasks (`is_general`) | yes |
| 2026-11-15 | self | Appointments read "3:00 AM" for a 9:00 AM booking | seeded timestamps converted from the account's own timezone | yes |
| 2026-11-15 | self | A "checklists" beat was storyboarded, but the seeded `project_checklists` render nowhere on the project page | replaced with the work panel's dependency rows | yes |

## Risks

- **Claims that need evidence.** "Thirteen jobs", "seven designs" and the invoice
  states are true of the seeded staging account on the day of capture; the film
  must be re-shot if the data changes. The numbers are read from the screens
  shown, never typed.
- **Assets that need a licence.** The roof photographs are SunrAI's own
  landing-page assets (`public/landing/site-property-front.jpg`,
  `site-roof-overview.jpg`). Customer names and addresses are invented.
- **UI that must be the real product.** All of it. This form has no authored
  pixels; if the product changes, the film is stale and must be re-captured.
- **Anything generated.** Nothing is generated. The greeting line reads
  "Guillermovillegas" because that is the staging account's own handle; the
  opening camera frames below it rather than editing the name in.
- **Staging availability.** The film depends on `staging.sunrai.ai` answering
  during the capture. A capture that fails mid-run leaves a partial recording;
  the harness refuses to render a run whose beat log is incomplete.
