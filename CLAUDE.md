# Patient Pathways — prototype

Context for Claude Code. Read this fully before building. It carries decisions made
in design sessions that are NOT re-derivable from the code alone.

## What this is

A physical **card game**, prototyped here as a single-page static web app, that helps
ViiV field staff (account managers / MSLs) facilitate **shared decision-making (SDM)**
conversations with HIV physicians. The web prototype exists to **playtest the mechanic**
and to demo it live (GitHub Pages) — it mirrors a real paper deck.

Client: ViiV Healthcare Netherlands, via Happy Horizon. Live role-play demo target:
**Cycle Meeting, 24–25 September**.

## The one principle that governs every decision

**This is a NEUTRAL SDM + barrier-diagnosis instrument. It is NOT a persuasion / promotion tool.**

- There is **no "correct" treatment route**. The tool surfaces the complexity and
  unpredictability of patient context; it does not steer toward Long-Acting (LAM/VnR).
- SDM's job is to find the **right care per patient**, NOT to identify LAM candidates.
  If the mechanic ever starts funnelling toward "is this patient suitable for LAM",
  that is the known failure mode (a testrun collapsed into a patient-eligibility game).
  Reject that framing in copy, scoring, and flow.
- LAM adoption is a downstream *consequence* of removing barriers and better
  conversations — never the target the tool points at.
- Scoring (if any) measures **process quality**, never clinical outcome. Do not imply
  a right answer with numbers.

Why neutrality is non-negotiable: (1) compliance — a promotional tool given to HCPs
falls under the Gedragscode Geneesmiddelenreclame / IGJ oversight, and MSLs must stay
non-promotional; a neutral instrument is the only version Medical Affairs can touch;
(2) physicians are already willing to prescribe (89% in ViiV's 2026 NL qual tracking)
but only ~2% of patients convert — the gap is operational barriers, not persuasion;
if the tool feels like selling, HCPs disengage and you capture nothing.

## Architecture: stable core + swappable modules

The deck is **modular by construction**. One adaptive deck — NOT separate decks per
segment, NOT expansion sets on day one.

**CORE (stable, coherent, print/ship now, no regulatory blocker):**
- SDM conversation loop + prompt cards
- Patient **base profiles** — pre-built, clinically COHERENT, validated units
  (archetype + plausible context). Never randomly composed from loose category draws
  (that produced a "24yo with age-related osteoporosis" that broke credibility).
- Twist / Life-Event cards — drawn on top AFTER a commitment; freely combinable because
  they are life events, not clinical facts.

**MODULES (volatile, slot-in, updatable without reprinting the core):**
- ART medicine content — **compliance-gated, ViiV-supplied**. Leave as marked
  placeholders. Do NOT invent clinical claims. (A 6-monthly injectable is anticipated;
  it will arrive as a new medicine module.)
- Implementation routes / **VoReZorg** — funding/logistics, changes over time.
- Barriers + facilitators — centre-specific, evolves as facilitators are built.
- Comorbidity clinical bodies — **ViiV-supplied**, left as placeholders.

The same seam solves three problems at once: coherence, compliance/content-readiness,
and a changing market. Keep the seam clean — blur it and the incoherence bug returns.

## The round loop (the mechanic)

1. **Case is dealt** — a coherent base profile is *given*, never assembled by the player.
2. **Conversation** — prompts drive an SDM dialogue about the patient's life/context.
3. **Provisional choice** — how the player would shape the care conversation
   (neutral — NOT "pick LAM").
4. **Twist revealed** — a Life-Event card, revealed only after the commitment.
5. **Does it hold?** — reflect whether the decision survives the new context; capture
   the barrier that surfaced.

Playing the loop *is* the barrier-elicitation instrument: where the conversation stalls
or a route feels blocked = a barrier location. Capture it (this feeds the barrier map →
which facilitators to build).

## Segments (entry point, not separate games)

Same loop, different emphasis/depth:
- **Sceptics / Distractors** → enter via barriers & logistics (treatment path first).
- **Believers / Advocates** → move faster to patient profiles & SDM depth.

**First build target for the Cycle Meeting: the sceptic / barrier module.** It is the
least tested and most at risk of sliding back into a product pitch, so it's the safest
place to get neutrality right first. Build ONE fully worked demo module, not the whole deck.

## Barriers in the NL landscape (from ViiV 2026 qual tracking — the backbone, don't re-brainstorm)

Organisational/capacity (strongest): nurse shortage; in-clinic admin space/planning;
waitlists. Structural/logistics: 2-monthly schedule + strict ±7-day window; cold chain.
Financial: perceived costlier once homecare/nursing added; "cost-critical" duty.
Professional/attitude: fear of virologic failure/blips; uncertainty identifying the
"right" patient; clinical inertia. Patient-suitability (eligibility–suitability gap):
appointment reliability (#1 exclusion), high BMI, unknown resistance/genotype,
contact-frequency mismatch (stable patients seen ~2x/year — 2-monthly "medicalises"),
travel/work. Market-readiness: HCPs in "waiting mode" for 6-monthly, infrastructure
investment on hold. NL differs from international assumptions — don't import those.

## Design / build conventions

- **Aesthetic: stark monochrome, ink-minimising.** No colour. Cards differentiate by
  **border style, line-art outline symbol, and index-tab position** — not colour.
- Cards mirror the physical print spec: **85×120 mm** (portrait, ratio ~0.708),
  2×2 per A4, single-sided, 100% actual size. On screen, keep card proportions ~0.708.
- **Stack:** vanilla static HTML/CSS/JS, single file where reasonable, **no build step**
  (must serve as-is from GitHub Pages). No framework required.
- Language: prototype UI is **Dutch** (used in NL sessions). Final card-FACE content is
  English per project convention; Figma briefs are English. Keep placeholder clinical
  content clearly marked and empty pending ViiV input.
- Compliance guardrail for you: never write invented clinical/product claims into cards.
  Anything about medicine efficacy, comorbidity management, or LAM benefit stays a
  labelled placeholder ("[ViiV-supplied — pending compliance]").

## What "done for the CM" looks like

Show at 24–25 Sept: the resolved sceptic/barrier route, the segment logic, ONE playable
module to actually rehearse with in the room, plus a build brief with a timeline for the rest.

## People (for tone/context only)

Ian (moderator/process design), Koen & Isabelle (agency, aligned on the above),
Andrada (ViiV Marketing), Michael (ViiV Medical Affairs — clinical validation & compliance),
Hiskya (ViiV PA/GA — critical adviser). Marjolein/Hans (copy), Bianca (design).
