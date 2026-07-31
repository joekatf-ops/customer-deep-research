# Master Research Report: Locked Format Spec (v5)

The canonical worked example is `examples/master-research-report-example.html` (Cloudnite run, June 2026). Copy its full `<style>` block and page structure, swap the content. If a draft does not visually match the example, it is off-spec.

## Page setup

- A4 landscape via `@page { size: A4 landscape; margin: 42px 34px 46px; }`.
- White body background (`#ffffff`). Cream is an accent only.
- Running header via `@top-left` ("MASTER RESEARCH REPORT") and `@top-right` ("<PRODUCT CATEGORY> · <MONTH YEAR>").
- Footer: brand mark at `@bottom-left` (`assets/brand-mark-small.png`, pre-scaled to 16px tall) and page counter at `@bottom-center`.
- Cover is a named page (`page: cover`, margin 0): baked PNG background (`assets/cover-bg.png`), white brand wordmark 40px top-left **wrapped in a div**, 104px solid-white title "Master Research Report.", emerald divider + subhead (market, input link, date), INSIDE meta block bottom-right.
- The bundled `assets/brand-wordmark-white.png` and `assets/brand-mark-small.png` are placeholders. Swap them for your own white wordmark and small logo mark to brand the report.
- One section per page: each section after the first starts with `<div class="ppage"></div>` (page-break-before). A section too big for one page is split into two deliberate pages at a logical boundary (e.g. matrix / dossier).

## Brand tokens

Night Green `#003C3C`, Night Green Deep `#002626`, Emerald `#00DE83`, Cream `#F7F4EF` (accents only), Ink `#1A1A1A`, Soft Ink `#4A4A4A`, hairline `rgba(0,60,60,0.22)`. Poppins only. These are the report's default tokens; swap them for your own brand palette if you want, but keep the contrast relationships. Title Case headings ending in a period. No em dashes, no emoji, no exclamation marks except inside verbatim quotes. Report voice: third person, declarative, no reader address, no marketing speak.

## Tables (the core element)

- Full width, `border-collapse: collapse`, outer `0.6px` hairline border.
- Header row: Night Green background, cream 8.5px uppercase tracked text, vertical separators at 25% cream.
- Cells: 10.5px, hairline bottom AND right borders (column lines are required), white background, top-aligned.
- Cell classes: `.k` key cell (semibold night green), `.c` centered, `.q` italic night green for verbatim quotes, `.win` emerald-tint highlight for winners / current stage / recommended rows (apply to every cell to highlight a full row).
- Bullets inside cells use the small emerald-square list (`td ul li`).
- `thead` repeats automatically if a table crosses pages; avoid that by sizing sections to their page.

## Section order (one page each unless noted)

1. **Executive Summary.** Dark callout with the one-sentence test ("The [named product], the only [item] with [named mechanism], made for [person] who [pain]"), then the brand-in-one-table: Market, Persona, Problem space, Mechanism, Offer structure, The gap, Sophistication.
2. **The Problem Space.** 5 problem angles x (verbatim parent/customer quote, search behaviour, entry rung, concept role) + READ callout tying all angles to the one mechanism.
3. **Demand Signals by Country.** Keyword x country volume table (US/UK/CA/AU/NZ + competition + bucket), `.win` on standout cells, below-threshold rows kept with explanatory colspan, small-note for source caveats, reading bullets (spread verdict, standout wedge, geo notes, CPC range).
4. **Keyword Trend, 5 Years.** Full-width SVG line chart of Google Trends for the most generic term: emerald polyline + 13% emerald area fill, baseline axis, year tick labels, peak annotated with dot + label. Below: average-interest-by-year table with the breakout row highlighted, then bullets (what the breakout means, seasonality, production note). Chart recipe: downsample weekly to monthly means, x evenly spaced, y scaled 0-100.
5. **Awareness Ladder with Messaging.** 5 rungs x (they type / see, "What we say": 5 to 7 ACTUAL copy lines in quotes, brand voice, placeholders like `[X]` for unearned numbers). No destination column, no abstract rules.
6. **Market Map.** Competitor table: brand, price, positioning and mechanism, strengths / weaknesses, links column with store URL + Meta Ad Library link only.
7. **Pricing Tiers and the Gap + Market Sophistication** (shared page). Tier table with our tier row highlighted; dark THE GAP callout; sophistication table of Schwartz stages 1-5 with the market's current stage row fully highlighted and labelled "THE MARKET IS HERE".
8. **Avatar Scoring Matrix.** Criteria x candidates with scores, totals, role row; winner column highlighted; kill-rule and evidence bullets.
9. **Master Avatar Dossier + Ranked Objections** (shared page). Dossier field table; objections table (#, objection verbatim, answer, where).
10. **The Named Mechanism.** Six-step chain table (numbered emerald step column) + name candidates table with recommended row highlighted.
11. **Claim Ceilings + Benefits Mapped to Desires** (shared page). Two-column approved vs banned claims; feature/benefit/desire(verbatim)/LF8 table.
12. **LF8 Map.** All 8 drives x relevance x usage; primary drive row highlighted.
13. **Offer Architecture.** 1-2-3 pack table (price, per unit, saving, shipping=Free, gifts, role) with the pre-selected pack highlighted; offer rules bullets (guarantee, gifts kill objections, discount discipline, honest urgency, post-purchase OTO, anchors).
14. **Necessary Beliefs.** 8 rows: belief, stage, proof, placement.
15. **Testing Architecture: Concepts vs the Hero.** Short paragraph (ads discover, store converts one person; bridge advertorials; outperformance triggers a research review) + concept table with a rowspanned hero-locked column. No promotion rules section.
16. **Voice of Customer Bank.** Category counts vs floors table (state shortfalls plainly), sample verbatim rows table, rules bullet.
17. **Run Notes, Gaps, and Sources.** Status table of tooling gaps and checkpoint decisions; sources table with links.

## Charts

Inline SVG only (no chart libraries; weasyprint renders SVG natively). Solid emerald stroke 2.5px, optional `rgba(0,222,131,0.13)` area polygon, hairline baseline, 8.5px soft-ink axis labels, night-green annotation text. No gradient fills on text anywhere in the document.

## QA before delivery

1. Rendered page count equals planned `.ppage` + cover count exactly.
2. Zero U+2014 em dashes.
3. Every quote has a source; every unknown number is a `[placeholder]`, not an invention.
4. Column separators visible on every table.
5. PNG-preview the cover, the demand table, the trend chart, and one copy page before presenting.
