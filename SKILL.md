---
name: customer-deep-research
description: Deep customer and market research engine for validated DTC products. Takes a competitor link or Alibaba link as input and produces the Master Research Report, a locked-format PDF covering the problem space, per-country demand signals with 5-year trend charts, awareness ladder with ready-to-use copy lines, market map with competitor links, market sophistication staging, scored avatar matrix, named mechanism with claim ceilings, LF8 map, 1-2-3 pack offer architecture, necessary beliefs, concept-testing architecture, and a verbatim Voice of Customer bank. Use this skill whenever the user shares a competitor URL, Alibaba link, or product to research, or says anything like "research this product", "run deep research on", "build the research report", "do the customer research for", "analyse this market", "create the master sheet for", or wants market research, customer research, avatar research, offer research, or a research report for a brand or product.
---

# Customer Deep Research

Produces the **Master Research Report**: one evidence-based PDF with everything needed to build a single-hero-product brand. Runs once per validated product. The thesis it serves: take a familiar boring item, re-engineer it around ONE named mechanism, aim it at ONE emotionally loaded problem, for ONE specific person nobody is speaking to, sell it premium.

Three principles govern every stage:

1. **Evidence over vibes.** Every quote verbatim and sourced. Every avatar score cites evidence. Every claim respects a ceiling. Where data ran thin, say so loudly in the report; never pad, never invent. Numbers that do not exist yet are written as placeholders like `[X] reviews`.
2. **Fail loudly.** Hard minimums exist (quote counts, keyword coverage). If a gate fails, stop and tell the user what is thin instead of writing around it.
3. **One person.** The report converges on one master avatar, one named mechanism, one recommended offer. Breadth lives in the concept-testing section, not in the core.

## Intake

The user opens with a competitor link (most common), an Alibaba link, or a product description. Collect (ask only for what is missing):

- The link(s). Fetch them first; extract product, pricing, offer structure, claims, disclaimers, review counts.
- Persona hypothesis: who this product most plausibly serves.
- Target geos: default is the big 5 (US, UK, CA, AU, NZ).
- Price intent, if the user has one.

If the product cannot articulate even a candidate mechanism, stop: it fails the thesis test before research spend.

## Pipeline

Run the stages in order. Three checkpoints pause for the user's decision via AskUserQuestion; everything else runs autonomously. Track stages with the task list. Tool specifics, actor names, and fallbacks live in `references/pipeline-tools.md`; read it before Stage 1.

**Stage 1, Demand.** Pull monthly Google volumes for 8 to 12 head terms across each target country. Gate: at least 5 terms must return real volumes per country; if not, widen to more generic head terms (category nouns, problem nouns) until they do. Pull the 5-year Google Trends series for the most generic category term (and other head terms when budget allows). Classify the awareness spread: healthy / brand-locked / early / commodity.

**Stage 2, Market map.** TrendTrack first if connected, then live web. 5 to 8 direct competitors: price, positioning, mechanism, strengths, weaknesses, store URL, Meta Ad Library search link. Indirect competitors (status quo, professional service, DIY, budget version). Pricing tiers and the gap. Audit incumbent trust signals honestly; fabricated proof on competitor sites is white space, record it.

**Stage 3, Review mining.** Scrape Amazon reviews (full text, competitor and adjacent ASINs), Reddit threads in the category's subreddits, Trustpilot on direct competitors. Build the Voice of Customer bank: verbatim, sourced, dated, tagged across six categories. Floors: Pain 30, Outcome 30, Objection 20, Comparison 20, Identity 15, Discovery 15 (130 total). Below floor = keep mining; if sources are exhausted, flag the shortfall in the report and at the checkpoint. Competitor-site reviews are language only, never proof.

**Stage 4, Avatars.** From the evidence, list 4 to 6 candidates and score each 1 to 5 on: pain severity, urgency, readiness to act, ability to pay, desire strength, objection friction (5 = low). Kill rules: ability-to-pay 1 is dead; readiness 2 or less means brutal CAC. Draft the winner's dossier (life, 2am reality, tried-and-failed, fear, dream outcome, home rung, channels) and ranked objections with answers.
**CHECKPOINT 1:** present the matrix and dossier; the user approves or re-scores.

**Stage 5, Sophistication and mechanism.** Stage the market 1 to 5 (Schwartz) from live ad claims: which claims are burnt, who holds each stage, where the market sits today. Build the six-step mechanism chain (root cause, effect, symptoms, what the product does, why that works, outcome) with a source per step. Generate 3 to 5 mechanism name candidates with rationale and risk. Write the claim ceilings table: approved phrasings vs banned claims; in any health-adjacent or kids category, the incumbent's own disclaimer marks the regulatory line.
**CHECKPOINT 2:** the user picks the name (note it needs a trademark sanity check).

**Stage 6, Benefits and LF8.** Feature, benefit, desire table where every desire is verbatim from the bank where possible. Full LF8 map: all 8 drives, relevance rating, how the brand uses each, with one drive marked primary.

**Stage 7, Offers.** Standard structure: 1, 2, and 3 packs. Free shipping on every order. Free gifts unlock at 2-pack and 3-pack (each gift must kill a ranked objection). Free guide on all orders. Deepest discount only at the 3-pack. Named guarantee on every pack. One post-purchase OTO (never a fourth PDP option). Price anchors from the real pricing gap (professional service cost, failed cheap alternatives, per-day cost). Honest urgency only: real batches, real counts.
**CHECKPOINT 3:** the user approves pricing and gift mix.

**Stage 8, Beliefs and testing architecture.** The 8-belief purchase chain (belief, stage, proof, placement; order is binding). The concept-testing table: 4 to 6 ad concepts (persona x problem), example hook each, destination each, and the hero-locked column (PDP, homepage, welcome flow always written to the master avatar; concepts get bridge advertorials).

**Stage 9, Build the report.** Read `references/report-template.md`, then build and render the PDF exactly to the locked format. QA before delivery: rendered page count equals planned page count (no silent overflow), zero em dashes, zero invented numbers, every quote sourced. Save the PDF and HTML to the project folder and present the PDF.

## The locked output

A4 landscape, white inner pages, branded cover (Lifestyle Brands wordmark by default; swap the files in `assets/` for your own), flowing table-led report, one section per page. Fourteen sections in this order: Executive Summary (one-sentence test + brand-in-one-table), Problem Space (5 problem angles with verbatim quotes), Demand Signals by Country, Keyword Trend 5 Years (hero chart + year table), Awareness Ladder with Messaging (actual copy lines per rung, 5 to 7 each), Market Map (links: store + Meta Ad Library), Pricing Tiers + Sophistication (current stage row highlighted), Avatar Scoring Matrix, Avatar Dossier + Objections, Named Mechanism (chain + candidates), Claim Ceilings + Benefits-to-Desires, LF8 Map, Offer Architecture, Necessary Beliefs, Testing Architecture, Voice of Customer Bank, Run Notes and Sources. No how-to page, no closer page, no promotion rules. Full spec, CSS, and chart recipe: `references/report-template.md`. Canonical example: `examples/master-research-report-example.html`.

## Honesty rules (the moat)

The reference brands in this space fake their trust layer: invented doctors, implausible review counts, resetting timers. The report treats that as the competitive gap, and the skill never reproduces it. Real counts or placeholders. Real experts or none. Real batch urgency or no urgency. A skeptical, research-driven buyer is the avatar in most premium niches; honesty converts them and compounds into the stage-5 identity position.
