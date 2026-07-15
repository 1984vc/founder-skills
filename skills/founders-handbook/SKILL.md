---
name: founders-handbook
description: Reference library of startup guides covering company formation, fundraising, equity mechanics, M&A, engineering, and taxes — written by the partners at 1984vc for early-stage founders.
license: CC-BY-ND-4.0
metadata:
  author: 1984 Ventures
  version: "1.0.0"
---

# 1984vc Founders Handbook

Practical guides for startup founders, written by the partners at [1984vc](https://1984.vc). All source documents are in `references/`.

Use this skill when a founder asks about fundraising mechanics, cap table math, co-founder dynamics, M&A exits, engineering practices, or tax strategy.

---

## Company Formation

### [Cap Table 101](references/cap-table-101.md)
The mathematical foundations of cap table ownership. Covers how new shares dilute existing holders, price-per-share calculation, priced rounds vs SAFEs, and how to model your ownership through multiple financing rounds. Essential reading before any fundraise negotiation.

### [Cap Table MCP](references/cap-table-mcp.md)
Live cap table calculations via the MCP at `https://startup-finance.1984.vc/mcp`. Use when a founder wants to model a real scenario — handles SAFEs, priced rounds, and options pool top-ups. Includes a worked example with two co-founders, YC, and a seed investor.

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
