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

- **Mode 1 — Treatment-path scan** (sceptics / undecided). **No patient.** The physician
  is the expert on their own practice; the AM listens and maps where the path pinches
  (capacity, scheduling & window, logistics/cold chain, funding/VoReZorg, follow-up).
  Non-teaching by construction. Output: barrier map.
- **Mode 2 — Patient case** (believers / advanced). A rich, coherent patient is dealt.
  Loop: patient → opening → explore → provisional approach → twist → does it hold.
  Output: reflection + the barriers the conversation exposes.

Modes are distinct LOOPS but must share one deck, one data model and one capture/log.
NEVER let modes diverge into separate content sets (that would be two decks, double the
compliance surface, and lose the reprint-free core). Both modes end in the same
barrier map — this preserves the phase-1 (diagnose) → phase-2 (activate) chain.

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
appear at the case's **Approach** step (`practicePanel()`), each with a neutral
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

- **Aesthetic: stark monochrome, ink-minimising.** No colour. Cards differentiate by
  border style, line-art outline symbol and index-tab position. Display face: Century
  Schoolbook stack (matches the deck's editorial identity); body: Helvetica/Arial.
- Cards mirror print spec **85×120 mm** (aspect-ratio 85/120). 2×2 per A4.
- **Stack:** vanilla static HTML/CSS/JS, single file, **no build step** — must serve as-is
  from GitHub Pages. `index.v1.html` is kept for reference only.
- State is in-memory; the barrier map is copied out via the clipboard button.
  Persistence/export is a sensible next feature (localStorage is fine on Pages).

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
