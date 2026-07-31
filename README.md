# customer-deep-research

A Claude skill that turns one competitor link into a complete customer research report for a DTC brand.

Built by [Joe](https://instagram.com/joekatf) at Lifestyle Brands. This is the exact research engine behind his own brand launches, free to take and run for yours.

You give it a competitor URL, an Alibaba link, or a product description. It runs a nine-stage research pipeline and delivers the **Master Research Report**: a locked-format PDF with everything needed to position, price, and launch a single-hero-product brand.

## What the report contains

Demand signals by country with real Google search volumes, a 5-year trend chart, the awareness ladder with ready-to-use copy lines per rung, a market map with competitor store and ad library links, pricing tiers and market sophistication staging, a scored avatar matrix and full avatar dossier, a named mechanism with claim ceilings, the LF8 desire map, a 1-2-3 pack offer architecture, the 8-belief purchase chain, a concept-testing plan, and a verbatim Voice of Customer bank built from real reviews and Reddit threads.

Every quote is verbatim and sourced. Every number is real or marked as a placeholder. The skill refuses to invent proof, because faked trust signals are exactly the gap it teaches you to exploit honestly.

## How it runs

Stage 1 pulls keyword volumes and Google Trends for your target countries. Stage 2 maps direct and indirect competitors. Stage 3 mines Amazon, Reddit, and Trustpilot for 130+ tagged customer quotes. Stages 4 to 8 score avatars, stage the market, name the mechanism, and build the offer, pausing three times for your decisions. Stage 9 renders the PDF.

A finished example is in `examples/master-research-report-example.html`.

## What you need

- Claude with the ability to run skills: [Cowork](https://claude.com) in the Claude desktop app, or [Claude Code](https://claude.com/claude-code).
- The **Apify** connector, used for keyword volumes, Google Trends, Amazon reviews, Reddit, and Trustpilot. A run costs a few dollars in Apify usage.
- Optional: the TrendTrack MCP for ad intelligence. The skill falls back to live web research without it.

## Install

**Claude desktop / Cowork:** download this repo (green Code button, then Download ZIP), unzip it, and upload the folder as a skill in your Claude settings under Capabilities. Or grab `customer-deep-research.skill` from this repo and upload that file directly.

**Claude Code:** copy the folder into your skills directory:

```bash
git clone https://github.com/joekatf-ops/customer-deep-research.git
cp -r customer-deep-research ~/.claude/skills/customer-deep-research
```

## Run it

Open a new session and say:

```
Research this product: <competitor or Alibaba link>
```

Answer the intake questions, then let it run. It pauses at three checkpoints: avatar selection, mechanism naming, and offer pricing.

## Make it yours

The report ships with the Lifestyle Brands cover marks. To put your own brand on it, replace `assets/brand-wordmark-white.png` (white logo, shown on the dark cover) and `assets/brand-mark-small.png` (small footer mark). The colour tokens live in `references/report-template.md` if you want to change the palette.

## Questions

Joe posts brand-building breakdowns, including runs of this exact skill, on Instagram: [@joekatf](https://instagram.com/joekatf). DM him what you launch with it.

## License

MIT. Take it, use it, build brands with it.
