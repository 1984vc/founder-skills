---
name: 1984-founders-handbook
description: Practical startup guidance and cap-table modeling from 1984 Ventures. Use for company formation, fundraising, SAFEs, founder ownership and dilution calculations, priced rounds, option pools, co-founder dynamics, M&A, engineering, taxes, or saving and sharing an interactive cap table.
license: CC-BY-ND-4.0
metadata:
  author: 1984 Ventures
  version: "2.0.0"
---

# 1984vc Founders Handbook

Practical guides and tools for startup founders, written by the partners at [1984vc](https://1984.vc). All supporting documents are in `references/`.

Use this skill when a founder asks about fundraising mechanics, cap-table math, co-founder dynamics, M&A exits, engineering practices, or tax strategy. This is the repository's only skill; cap-table calculation is part of the handbook rather than a separate skill.

## How to use this handbook

1. **Explain the concept.** Read the relevant handbook reference and answer in plain language.
2. **Model the numbers.** For a concrete ownership or dilution scenario, use the cap-table CLI described below instead of doing complex share math by hand.
3. **Save and share when useful.** If the founder wants an editable worksheet or shareable link, use the hosted Startup Finance API.
4. **State assumptions.** Distinguish pre-money from post-money valuation, issued from unused options, and pre-money from post-money SAFEs. Ask when a missing term can materially change the result.

## Cap-table calculations

Use [`@1984vc/cap-table`](https://www.npmjs.com/package/@1984vc/cap-table) for existing ownership, SAFE conversion, priced rounds, and option-pool refreshes. Version `0.2.1` or later is required for correct MFN adoption in priced rounds.

| Founder needs | CLI command |
|---|---|
| Existing shareholders only | `existing` |
| SAFEs but no priced round | `estimated-pre-round` |
| Ownership immediately before a known priced round | `pre-round` |
| Full post-round ownership and dilution | `priced-round` |

Inputs can be an inline JSON argument, stdin, or a JSON file:

```bash
npx @1984vc/cap-table@^0.2.1 priced-round '{
  "preMoneyValuation": 20000000,
  "common": [
    {"name": "Founder 1", "shares": 5000000},
    {"name": "Founder 2", "shares": 5000000}
  ],
  "safes": [
    {"name": "Seed SAFE", "investment": 1000000, "cap": 10000000, "discount": 0, "conversionType": "post"}
  ],
  "seriesInvestors": [
    {"name": "Series A Lead", "investment": 5000000}
  ],
  "targetOptionsPct": 0.10
}'
```

CLI percentages are decimals: `0.10` means 10%. Check the exit code and treat the JSON output as the calculation source of truth.

For founder shorthand, YC's standard deal, complete schemas, outputs, and examples, read:

- [Cap-table calculator workflow](references/cap-table-calculator.md)
- [Founder shorthand and common terms](references/cap-table-common-terms.md)
- [TypeScript library reference](references/cap-table-library-api.md)

### Save and share a cap table

When a founder wants a link they can reopen, edit, or send to a co-founder or investor, call `https://startup-finance.1984.vc/mcp`:

- `estimate_pre_round` — SAFE-only worksheet
- `calculate_cap_table` — priced-round worksheet
- `read_worksheet` — resume a shared worksheet
- `update_worksheet` — update it with its edit key

Both calculation tools save the model and return a worksheet URL. Always return that URL to the founder. The hosted API uses whole-number percentages (`10` means 10%), unlike the CLI. See [Startup Finance API](references/startup-finance-api.md) for request schemas and examples.

---

## Company Formation

### [Cap Table 101](references/cap-table-101.md)
The mathematical foundations of cap table ownership. Covers how new shares dilute existing holders, price-per-share calculation, priced rounds vs SAFEs, and how to model your ownership through multiple financing rounds. Essential reading before any fundraise negotiation.

### [Cap Table Calculation and Sharing](references/cap-table-mcp.md)
Decision guide for calculating locally with `@1984vc/cap-table` or saving an editable worksheet through `startup-finance.1984.vc`.

### [How to Pick a Startup Idea](references/how-to-pick-a-startup-idea.md)
Strategy for finding startup ideas in the AI era. Argues against chasing large obvious markets; instead advocates for niche or offline industries where AI creates outsized leverage. Includes concrete portfolio examples.

### [Choosing Your Co-Founder](references/choosing-your-co-founder.md)
Why co-founder selection is one of the highest-leverage decisions a founder makes. Covers the most common mistakes, where to find co-founders, how to evaluate fit, and how to structure vesting agreements before committing.

### [How to Part Ways with Your Co-Founder](references/cofounder-departure.md)
A practical guide to handling co-founder separations without destroying the company. Covers the three root causes of founder conflict, the five steps of a clean transition, and how to reach a separation agreement that protects the business.

### [Founder Departure Impact on Cap Table](references/founder-departure.md)
How a departing founder's equity is treated differently depending on whether the seed round was a priced round vs. a SAFE. Includes worked cap table examples showing how forfeited shares redistribute to remaining holders.

### [Minimizing Founder Dilution](references/minimizing-founder-dilution.md)
Tactics for reducing Series A dilution beyond just executing well. Focuses on generating a second term sheet (BATNA) as the single most effective negotiating lever, with guidance on how to create competition without burning bridges.

---

## Raising Your Seed

### [Introduction to SAFEs](references/intro-to-safes.md)
The history and mechanics of SAFE instruments from YC's 2013 original to the 2018 post-money revision. Explains why SAFEs replaced convertible notes, the two key terms (cap and discount), and what rights SAFE holders have before conversion.

### [Pre-money vs Post-money Conversion](references/pre-money-vs-post-money-conversion.md)
The critical difference between pre-money and post-money SAFEs when multiple rounds are stacked. Shows with worked examples how post-money SAFEs give investors a fixed ownership regardless of round size, while pre-money SAFEs dilute differently across rounds.

### [SAFE vs Priced Round](references/safe-vs-priced-round.md)
When to use a SAFE versus a priced equity round. SAFEs are simpler, more flexible, and preserve founder control; priced rounds are appropriate when investors require a board seat or when raising a large seed. Covers trade-offs for both sides.

### [SAFE Side Letters](references/safe-side-letters.md)
What investors typically request in SAFE side letters and which terms are reasonable vs. problematic. Covers pro-rata rights (recommended formula language), MFN clauses (levels of complexity and risk), and information rights. Includes recommended standard language.

---

## Raising Your Series A

### [How to Nail Your Series A Deck](references/series-a-deck.md)
Slide-by-slide guidance for building a Series A pitch deck. Key principles: one message per slide, 15 slides max, story-first structure. Covers what investors look for at each section and links to a sample deck template.

### [Impact of Series A on Cap Table](references/raising-your-series-a.md)
Mechanics of how a Series A round reshapes the cap table. Covers option pool top-up (why it comes from founders, not investors), pro-rata rights exercise by seed investors, and the math behind typical Series A ownership targets.

### [Selling Secondaries](references/selling-secondaries.md)
How and when founders can sell personal shares to investors. Explains the mechanics (no dilution to other shareholders), when it's appropriate (typically Series C+, sometimes Series B for top performers), how to find buyers, and the board consent process.

### [Structured and Down Rounds](references/structured-and-downrounds.md)
What to do when a company can't raise at its last valuation. Explains structured rounds (dirty terms like superior liquidation preferences, guaranteed returns) vs. clean down rounds. Argues that down rounds are almost always better for founders and existing shareholders than structure.

---

## Engineering

### [Engineering Best Practices at Seed Stage](references/eng/best-practices-seed.md)
Non-negotiable engineering discipline for seed-stage companies. The core argument: testing is a competitive advantage, not a luxury. Covers critical-path tests, regression tests, and integration tests as the foundation that lets engineers move fast post-Series A without rewriting everything.

### [Open Source Content Marketing: Lessons from PostHog](references/eng/open-source-playbook-posthog.md)
How open source startups can drive discovery through content. Based on PostHog's playbook: "alternatives to X" articles, search-optimized content targeting engineers at decision points, and building a content engine that compounds over time. Practical and immediately actionable.

### [Why Your Open Source Project Needs Telemetry](references/eng/open-source-telemetry.md)
The case for privacy-respecting telemetry in open source projects. Argues that without usage data, maintainers build in the dark. Covers how to collect meaningful metrics (feature usage, error rates, performance) without betraying user trust, and how to communicate the policy to the community.

---

## Mergers and Acquisitions

### [How to Sell Your Startup](references/mergers-and-acquisitions/how-to-sell.md)
A step-by-step guide to running an M&A process. Covers when to hire a banker vs. go direct, how to build a buyer pipeline, managing parallel conversations, negotiation tactics, and how to handle exclusivity and LOI stages. Emphasizes that companies are bought not sold — but preparation matters.

### [Legal Considerations for M&A](references/mergers-and-acquisitions/legal-considerations.md)
The legal preparation required before entering an M&A process: engaging counsel, conducting sell-side due diligence, cleaning up cap table and corporate records, IP assignments, and employment matters. Aimed at founders who have never been through a sale before.

### [Structuring M&A](references/mergers-and-acquisitions/structuring.md)
The three ways to structure an acquisition — asset purchase, stock purchase, and merger — with plain-language explanations of what each means for the buyer and seller. Covers the commercial and tax trade-offs of each structure and when each is typically used.

### [Terms to Negotiate in an M&A Transaction](references/mergers-and-acquisitions/terms.md)
The key provisions in an acquisition agreement: consideration, purchase price adjustments, earnouts, escrow, governance, representations and warranties, closing conditions, and indemnification. Distinguishes commercial terms (founder's job) from legal terms (counsel's job).

---

## Taxes

### [QSBS: A Tax Strategy Worth $15 Million](references/taxes/qsbs.md)
How Qualified Small Business Stock (Section 1202) lets founders exclude up to $15M in gains from federal capital gains taxes. Updated for the July 2025 One Big Beautiful Bill Act which increased the exclusion cap and reduced the holding period. Covers eligibility requirements, state treatment, and planning considerations.
