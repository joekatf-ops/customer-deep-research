# Pipeline Tools and Fallbacks

The exact tools per stage, with known limitations from the validation run (Cloudnite, June 2026). When a tool is unavailable, use the listed fallback and record the gap in the report's Run Notes section.

## Stage 1: Demand

**Volumes per country:** Apify actor `doesaiknow/doesaiknow-keyword-metrics-apify`.
- Input: `{"keywords": [...], "country": "us|gb|ca|au", "language": "en"}` (country lowercase).
- Returns Google volume, CPC, competition, trend, and a 12-month monthly series per keyword.
- Limitation: NZ is not supported. Use a DataForSEO-based actor with NZ location codes for NZ, or mark the NZ column `n/a` with a note. Never copy AU numbers into NZ.
- Long-tail kid/niche phrases often return null (below Ads reporting threshold). That is data, not failure: note "below threshold, demand visible in autosuggest and forum volume" and keep the row.
- Gate: at least 5 keywords with real volumes per country. If short, add more generic head terms (category noun, problem noun, adjacent product noun) and rerun.

**5-year trend:** Apify actor `apify/google-trends-scraper`.
- Input: `{"searchTerms": [...], "timeRange": "today 5-y", "geo": "US", "skipDebugScreen": true}`.
- The timeline is weekly (~260 points per term) and very large. Fetch ONE term at a time and chart the most generic category term first. Downsample to monthly means for charting.
- The breakout check matters: compare the last 6 months against the 4-year baseline. A flat baseline with a recent spike means a paid-ads wave is creating demand right now; that is a headline finding.

## Stage 2: Market map

- **TrendTrack MCP first** when connected (product and ad intel). If not connected, note it in Run Notes and use live web research.
- Web fetch competitor stores directly (PDP, pricing, guarantee, disclaimer pages).
- Meta Ad Library link format per brand: `https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=ALL&q=<brand>`.
- WebSearch for pricing roundups and the adult/adjacent analog brands (they show where the playbook and its trust ceiling are heading).

## Stage 3: Review mining

**Amazon (primary quote source):** Apify actor `web_wanderer/amazon-reviews-extractor`.
- Input: `{"products": ["ASIN1", "ASIN2"], "limit": 3, "sort": "recent", "region": "amazon.com"}` (products is an array of plain ASIN strings or URLs; limit is pages, ~10 reviews per page).
- Do NOT use `khadinakbar/amazon-reviews-scraper`: it returns ratings with null review text (verified broken June 2026).
- Find ASINs via WebSearch (`<competitor> site:amazon.com /dp/`).

**Reddit:** Apify actor `prodiger/reddit-scraper`.
- Input: `{"searchQuery": "<pain phrase>", "searchSubreddit": "<sub>", "sort": "relevance", "timeFilter": "all", "includeComments": true, "maxPostsPerSource": 25, "maxCommentsPerPost": 20}`.
- Search the pain language, not the product ("snoring adenoids" outperformed "child snoring pillow"). Run 2 to 4 targeted queries across the category subreddits.

**Trustpilot:** Apify actor `getwally.net/trustpilot-reviews-scraper`.
- Input: `{"startUrls": [{"url": "https://www.trustpilot.com/review/<domain>"}], "limit": 40}`.

**Tagging:** every quote gets QUOTE / SOURCE / DATE / CATEGORY (Pain, Outcome, Objection, Comparison, Identity, Discovery). Verbatim only; do not fix grammar; do not translate "stiff neck" into "cervical discomfort".

## Stages 4 to 8

No external tools; these are synthesis stages run against the evidence. Frameworks (scoring criteria, Schwartz stages, LF8, value equation, belief chain) are embedded in SKILL.md and the report template. Checkpoints use AskUserQuestion with the live data in the question options.

## Stage 9: Render

- Build the HTML from `references/report-template.md` with assets from `assets/`.
- Render: `pip install weasyprint --break-system-packages` then `weasyprint` via python. Poppins must be available (it is in the Cowork sandbox).
- QA loop: rendered page count must equal the number of planned pages. If higher, a section overflowed: trim rows or split the section onto its own page, re-render. Verify zero em dashes (U+2014) and that the cover wordmark is wrapped in a `<div>` (bare img inside the flex cover stretches).
- Convert pages to PNG (`pdftoppm -png -r 45`) and visually inspect the cover, one table page, and the chart page before delivery.
- Save PDF + HTML + assets to the project folder; present the PDF.
