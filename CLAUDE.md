# ViiV deck — prototype

Context for Claude Code. Read this fully before building. It carries decisions made
in design sessions that are NOT re-derivable from the code alone. v2 — 1 Sept 2026.

## What this is

A physical **card game**, prototyped here as a single-page static web app, that helps
ViiV field staff (account managers / MSLs) support HIV physicians around
**shared decision-making (SDM)** and the barriers in their treatment path. The web
prototype exists to **playtest and demo live** (GitHub Pages); it mirrors a real paper deck.

Client: ViiV Healthcare Netherlands, via Happy Horizon. Live demo target:
**Cycle Meeting, 24–25 September 2026** (three weeks from v2).

## The one principle that governs every decision

**This is a NEUTRAL SDM + barrier-diagnosis instrument. It is NOT a persuasion / promotion tool.**

- There is **no "correct" treatment route**. The tool surfaces complexity of patient
  context; it does not steer toward Long-Acting (LAM/VnR).
- SDM's job is the **right care per patient**, NOT identifying LAM candidates. If the
  mechanic starts funnelling toward "is this patient suitable for LAM", that is the known
  failure mode (a testrun collapsed into a patient-eligibility game). Reject it in copy,
  scoring and flow. LAM adoption is a downstream *consequence* of removing barriers,
  never the target the tool points at.
- Scoring (if any) measures **process quality**, never clinical outcome.

Why: (1) compliance — a promotional tool for HCPs falls under the Gedragscode
Geneesmiddelenreclame / IGJ; MSLs must stay non-promotional; a neutral instrument is
the only version Medical Affairs can touch. (2) Physicians are already willing (89%
in ViiV's 2026 NL qual tracking) but ~2% of patients convert — the gap is operational
barriers, not persuasion. If it feels like selling, HCPs disengage and you capture nothing.

## v2 decisions from the September workshop (supersede v1)

### 1. Two separate play MODES, chosen at the start — over ONE shared deck
Playtests showed "one loop with different emphasis" was too subtle: forcing barrier-
mapping and an SDM conversation into one loop produced the patient-identification spiral
and role drift. These are two jobs with two loops:

- **Mode 1 — Treatment-path scan** (sceptics / undecided). **No patient.** A CARD
  mechanic, not a form: five treatment-path cards laid as a row (capacity, scheduling &
  window, logistics/cold chain, funding/VoReZorg, follow-up). **The physician sorts each
  card** into loopt / knelt / weet niet with their own hands; only "knelt" opens the
  follow-up (what pinches, what would help) with that card's AM voice-over line.
  Optional implementation-route cards (in the clinic / home care / pharmacy — from the
  existing Implementation Routes category) mark which path steps the route leans on.
  This is the resolved form of the old "Sort & Defend" option: **physician sorts, AM
  asks.** Every sort state opens its own follow-up with its own AM line: knelt → what
  pinches + what would help (barrier + wanted facilitator); loopt → WHAT exactly is
  arranged (the mechanism another centre can adopt) + WHY it works here (the
  precondition it must also meet) — two fields, deliberately apart, because a facilitator
  without its precondition is a recipe without ingredients;
  weet niet → who would know (not a dead end: the next person to talk to, usually the
  nurse or pharmacist). Never treat "loopt" as a state to skip past.

  **Value design — the scan is an EXCHANGE, not extraction.** A busy physician has no
  reason to brief pharma; the scan must pay for its quarter-hour in the room, that day.
  The engine is reciprocity via peer implementation knowledge: ViiV is the only party
  that sees inside all treatment centres, so the AM comes to BRING ("here's how other
  centres solve this pinch"), not to collect. Consequences, all implemented and to be
  preserved: the opening line leads with what the AM brings; every "knelt" panel has a
  **peer slot** ("Zo pakt een ander centrum dit aan") — placeholder text until Michael
  validates anonymised examples, and when the bank is thin the AM says so honestly; the
  closing gives the map to the physician ("deze kaart is van jou"), commits to a DATED
  return on exactly these pinch points, and asks consent before sharing "what runs"
  with other centres. Each completed scan feeds the peer bank (that is why loopt
  captures what+why). Never revert the opener to "help us understand" — for sceptics
  that is the version that gets declined. Physical version: 5 path cards + 3 route cards + 3 zones on
  the table. Never let this drift back into a questionnaire the AM fills in.
- **Mode 2 — Patient case** (believers / advanced). A rich, coherent patient is dealt.
  Loop: patient → opening → explore → provisional approach → twist → does it hold.
  Output: reflection + the barriers the conversation exposes.

Modes are distinct LOOPS but must share one deck, one data model and one capture/log.
NEVER let modes diverge into separate content sets (that would be two decks, double the
compliance surface, and lose the reprint-free core). Both modes end in the same
barrier map — this preserves the phase-1 (diagnose) → phase-2 (activate) chain.

### 2a. The physician's screen states the SITUATION, never the technique
Screen copy addressed to the physician must never instruct how to doctor — no topic
lists ("ask about work, rhythm, travel..."), no conversational coaching ("ask about
life, not the pill"). The test: could the sentence hang on the wall of their own
consulting room without insulting them? Two reasons this is hard law: (1) a pharma
tool coaching a physician on anamnesis is patronising and backfires; (2) enumerating
the exploration topics is the ANSWER KEY to the hidden-facts mechanic — it turns open
questioning into a checklist. All teaching content lives in the Facilitator view
(voice-over) or in the patient's mouth ("I only tell you what you ask me"), never on
the physician's screen.

### 2. Roles: the physician ALWAYS sits in the physician's chair; the AM never does
v1's "conduct the SDM conversation" prompt put the AM in the doctor's seat. In the room
that reads as the rep teaching the doctor how to talk to patients — patronising, and it
backfired. Structural fix, not wording:
- The **HCP is the physician** practising. Prompts never tell them HOW to do SDM; they
  give them a patient to practise on.
- The **AM is facilitator + the patient's voice** — a sparring partner, not a teacher.
- The prototype has two **role views** (toggle in header, Mode 2 only): the physician
  sees the case + reflection prompts; the facilitator sees the patient's scripted voice,
  the hidden facts, the twist control and capture.

**Facilitator-first (v2.2 decision):** this app is in its base form the FACILITATOR'S
instrument. The physician plays the conversation without a screen (paper case card /
the spoken exchange); a digital physician view is **option 2**. Consequences: Mode 2
defaults to the Facilitator view; the toggle is labelled "Arts · preview" and the
physician view carries an option-2 note; the facilitator view is self-sufficient
(patient voice, hidden facts, optional notes at Explore, the choice capture at
Approach with its own facilitator lead, the barrier capture at Hold). Never make a
required capture live ONLY in the physician view.

### 3. Rich patient data — and the compliance distinction that allows it
Playtest: "we knew too little about the patient to hold an SDM conversation."
Profiles now carry demographics, medical picture, care use, lifestyle, and what the
patient values. The distinction that makes this compliant:
- **Case facts about a fictional patient** (suppressed since, BMI, genotype known/old,
  comorbidity, appointment reliability, visit frequency) are NOT product claims. They
  may be rich. They need **Michael's plausibility check** (coherence — the "24yo with
  age-related osteoporosis" lesson), nothing more.
- **Product specifics and benefits** (regimen name, efficacy, LAM advantages) stay
  labelled placeholders: "[ViiV — pending]". Do not invent them.
Deliberately, the suitability-relevant fields mirror the REAL NL barriers (appointment
reliability #1, BMI, genotype, 2×/year contact frequency, travel >4 weeks, needle fear)
so barriers surface naturally without the tool pushing anything.

### 4. Hidden-if-asked mechanic (rewards SDM without scoring right/wrong)
Each profile has **hidden facts** the patient only gives away when the physician asks
openly about life (work rhythm, relationship, travel, how they feel). The facilitator
reveals them on the right open question; unasked, they stay hidden — that IS the
exercise. Revealed facts surface in the physician's view and are logged. Keep this.

### 5. AM voice-over (the training layer)
Every step carries a **literal line the AM says out loud** plus a one-line *why*
(`m1_say` / `m2_say` in the `T` dictionary, rendered by `script()`). In Mode 1 it is
always shown (the AM is the only screen user); in Mode 2 it shows in the Facilitator
view only, never to the physician. `[naam]`/`[name]` is substituted with the profile
name. This is what trains AMs; keep lines neutral, non-teaching, in role where relevant.

### 6. The bridge: treatment-path scan → patient case
Barriers live at two levels. Mode 1 maps **practice-level** barriers (capacity, window,
logistics, funding, follow-up — fixed for the practice). The profile carries
**patient-level** barriers (appointment reliability, BMI, travel, needle fear). The SDM
conversation is where they meet. If a scan was played this session, its pinch points
appear at the case's **Approach** step (`practicePanel()`) — both what pinches AND
what runs (symmetric: a practice strength is also a given the patient weighs) — each with a neutral
"for the conversation" meaning (`SCAN[].m`). Framing is strict: a practice barrier is
**an input the patient weighs, not a verdict on an option** — the prompt asks "is this
a hurdle for THIS patient, or not?". Never let this become "so option X is unsuitable".
The scan stores `key` per item so the bridge can map back to `SCAN`.

### 7. Patient shuffle + three profiles
"Andere patiënt" cycles deterministically through profiles (Gabriel, Karen, Adrian —
three different barrier families: shift work/travel, carer/needle fear/2×yr, disclosure/
reachability). Facilitator can also cycle the twist. Add profiles in the same shape.

### 8. Bilingual (NL/EN) with a language switch
UI strings live in the `T` dictionary; content fields are `{nl, en}` objects resolved
by `L()`. Every new string/content item must have both. Dutch is the default (used in NL
sessions). Card-FACE final content is English per project convention.

## Architecture: stable core + swappable modules (unchanged)

CORE (stable, print now): SDM loop + prompts; patient base profiles (coherent,
validated); twist/life-event cards (freely combinable — events, not clinical facts).
MODULES (volatile, slot-in, updatable without reprinting): ART medicine content
(ViiV-gated; a 6-monthly injectable is anticipated); implementation routes/VoReZorg;
barriers + facilitators (centre-specific); comorbidity clinical bodies (ViiV-gated).

## Build conventions

- **Two visual layers — keep them apart.**
  *Physical cards* stay monochrome (no colour print): differentiation by border style
  (solid / dashed / double), line-art outline symbol and index-tab position. On screen
  they render navy-on-white with a sand tab; that is presentation, not a print promise.
  *Screen chrome* applies the ViiV brand subtly (60/30/10): warm off-white page
  (#FBF8F5), white panels, navy (#071D49) for all text/structure/borders, sand
  (#D7A27E) for warmth (header divider, card tab, patient voice, voice-over block),
  and Red Ribbon (#E40046) **only** as spotlight: primary CTA, selected toggle,
  focus ring, chosen answer option. Never red as a surface or for errors (validation
  hints are navy on sand-tint). Tokens live in `:root` as `--viiv-*`.
- **Type:** Inter (Google Fonts link) with a humanist system fallback; headings
  semibold navy, body regular, line-height ~1.6. Verify the licensed brand font with
  ViiV/GSK if 1:1 matching is required.
- **Icons:** simple line style, navy, rounded caps/joins. Radius 8–12px, light shadows.
- **Logo:** never draw or fabricate it. `assets/viiv-logo.svg` is a slot for the
  official red mark; the header hides it while the file is missing.
- **Tone (copy):** direct, hopeful, inclusive, person-first. Avoid "hiv-patiënten" as a
  category; "patiënt" is used only as the role in the consulting-room conversation.
- Cards mirror print spec **85×120 mm** (aspect-ratio 85/120). 2×2 per A4.
- **Stack:** vanilla static HTML/CSS/JS, single file, **no build step** — must serve as-is
  from GitHub Pages. `index.v1.html` is kept for reference only.
- State is in-memory; the barrier map is copied out via the clipboard button.
  Persistence/export is a sensible next feature (localStorage is fine on Pages).

## Accessibility — WCAG 2.1 AA baseline (maintain on every change)

Implemented and to be preserved: skip link + `<main>` landmark; progress rail as
`<nav>` with `aria-current="step"`; headings (h1 brand, h2 per screen, h3 card/panel
titles); decorative SVGs `aria-hidden`; `aria-pressed` on all toggle-like controls
(language, role, sort, route); errors as `role="alert"` that say what to do;
every input labelled (visible `<label for>` or `aria-label` — placeholders are not
labels); revealed facts announced via `aria-live="polite"`; visible focus everywhere
incl. `summary`; form/control borders use `--border-strong` (#5B6472, ≥3:1 non-text
contrast — never `--viiv-border` on interactive boundaries); touch targets ≥36px
(≥32px for small chips); `prefers-reduced-motion` respected; `document.documentElement.lang`
follows the language switch. Text contrast tokens are verified (navy/gray on warm white,
white on Red Ribbon ≈4.8:1) — re-check when introducing any new colour pairing.
Not yet done and worth a manual pass before the CM: screen-reader run (VoiceOver) and
200% zoom check.

## Scope for the Cycle Meeting (3 weeks)

Do NOT build the whole matrix. Foundation is in place (mode select, i18n, role views,
data model, both loops). Polish the mode that is role-played live in the room — likely
**Mode 2**, since the CM demo is a role-play — and keep Mode 1 clean and functional.
Get Michael/GA to check neutrality and the placeholder approach early. Test internally
at least once before 24 Sept.

## People (tone/context only)

Ian (moderator/process design), Koen & Isabelle (agency, aligned), Andrada (ViiV
Marketing), Michael (ViiV Medical Affairs — clinical validation & compliance),
Hiskya (ViiV PA/GA — critical adviser). Marjolein/Hans (copy), Bianca (design).
