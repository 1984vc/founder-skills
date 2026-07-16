# Common Terms & Founder Shorthand

> Reference for translating conversational founder language into CLI inputs.

## YC Standard Deal

YC invests $500,000 via two post-money SAFEs. Always model both, in this order, before any other SAFE investors:

| # | Investment | Cap | Discount | Type | Notes |
|---|-----------|-----|----------|------|-------|
| 1 | $125,000 | $1,785,714 | 0% | post-money | Gives YC exactly 7% at conversion |
| 2 | $375,000 | $0 (uncapped) | 0% | post-money + MFN | Adopts lowest cap from subsequent capped SAFEs |

### CLI JSON

```json
"safes": [
  { "name": "Y Combinator", "investment": 125000, "cap": 1785714, "discount": 0, "conversionType": "post" },
  { "name": "YC MFN", "investment": 375000, "cap": 0, "discount": 0, "conversionType": "post", "sideLetters": ["mfn"] }
]
```

> **Why $1,785,714?** $125,000 / 0.07 = $1,785,714. A post-money SAFE's ownership = investment / cap, so this cap gives exactly 7%.

> **MFN note:** The $375K tranche is an MFN (Most Favored Nation) SAFE. If the company later issues SAFEs with lower caps, the MFN tranche adopts the lowest cap. If no subsequent capped SAFEs exist, it converts at the round price (same as uncapped). Model with `sideLetters: ["mfn"]`.

---

## Founder Shorthand Glossary

### Ownership Splits

| Phrase | Meaning | How to model |
|--------|---------|--------------|
| "60/40" | Two founders, 60% and 40% | 10M total shares: `[{name: "Founder 1", shares: 6000000}, {name: "Founder 2", shares: 4000000}]` |
| "50/50" | Equal split | `[{name: "Founder 1", shares: 5000000}, {name: "Founder 2", shares: 5000000}]` |
| "I own 60, my co-founder owns 40" | Same as 60/40 | Same as above |

> **Share counts:** Founders typically start with 8-12M total common shares. 10M is the most common starting point. The exact count doesn't affect ownership percentages -- only the ratio matters. If the founder gives absolute share counts, use those. If they give percentages, assume 10M total and split accordingly.

### Valuation Shorthand

| Phrase | Meaning | preMoneyValuation |
|--------|---------|-------------------|
| "4 on 20 post" | $4M raise at $20M post-money | $16,000,000 (post - raise) |
| "4 on 20 pre" | $4M raise at $20M pre-money | $20,000,000 |
| "priced at 20" | $20M pre-money (usually) | $20,000,000 |
| "20 post" | $20M post-money | Depends on raise amount |
| "valuation of 20" | Ambiguous -- ask pre or post | Ask |

> **Key distinction:** "on X pre" means pre-money = X. "on X post" means post-money = X, so pre-money = X minus the raise. Always confirm if the founder doesn't specify.

### SAFE Terms

| Phrase | Meaning | CLI fields |
|--------|---------|------------|
| "did YC" / "went through YC" | YC's $500K standard deal | See YC Standard Deal above |
| "20% discount" | 20% discount off round price | `discount: 0.20` |
| "uncapped" / "no cap" | No valuation cap | `cap: 0` |
| "MFN" | Most Favored Nation | `sideLetters: ["mfn"]` |
| "post" / "post-money" | Post-money SAFE (YC standard) | `conversionType: "post"` |
| "pre" / "pre-money" | Pre-money SAFE (older, 2013) | `conversionType: "pre"` |
| "SAFE at 8M cap" | $8M valuation cap | `cap: 8000000` |

### Round Terms

| Phrase | Meaning | CLI field |
|--------|---------|-----------|
| "10% pool" / "option pool" | Target option pool percentage | `targetOptionsPct: 0.10` |
| "no pool" | No option pool refresh | `targetOptionsPct: 0` |
| "lead wrote 4M" | Lead investor invested $4M | `seriesInvestors: [{investment: 4000000}]` |
| "priced round" | Priced equity round (Series A+) | Use `priced-round` command |
| "no round yet" | SAFEs only, no priced round | Use `estimated-pre-round` command |

---

## Typical Terms by Stage

### Pre-seed / Pre-YC

- **Raise:** $150K-$1M (friends & family, angels)
- **Instrument:** Post-money SAFEs
- **Caps:** $3M-$8M
- **Discount:** 20% common, but many uncapped
- **Option pool:** Not yet created (0%)

### Seed (post-YC)

- **Raise:** $1M-$5M
- **Instrument:** Post-money SAFEs (occasionally priced)
- **Caps:** $8M-$15M
- **Discount:** 20% common for capped; 0% for uncapped/MFN
- **Option pool:** 10-15% if priced; 0% if SAFE-only

### Series A

- **Raise:** $5M-$15M
- **Instrument:** Priced equity round (preferred stock)
- **Pre-money:** $15M-$40M
- **Option pool:** 10% standard (created/refreshed as part of the round)
- **Board:** 1 founder, 1 investor, 1 independent (typical)

### Series B+

- **Raise:** $15M-$50M+
- **Pre-money:** $30M-$200M+
- **Option pool:** 5-10% refresh

---

## Worked Example: "60/40, did YC, round at 4 on 20 post"

**Founder says:** "My partner and I own 60/40, we did YC and then did a round at 4 on 20 post."

**Translation:**

| Phrase | Translation |
|--------|-------------|
| "60/40" | Two founders: 6M and 4M shares (10M total) |
| "did YC" | Two SAFEs: $125K @ $1.785M cap, $375K uncapped MFN |
| "round at 4 on 20 post" | $4M Series A at $20M post -> pre-money = $16M |
| (implied) | 10% option pool (Series A standard) |

**Clarifying questions to ask:**

1. How many total common shares do you have? (If unknown, assume 10M)
2. What's the lead investor's name? (For labeling)
3. Do you have an existing option pool? How many unissued options?
4. Any other SAFE investors besides YC?

**CLI command:**

```bash
npx @1984vc/cap-table@^0.2.1 priced-round '{
  "preMoneyValuation": 16000000,
  "common": [
    { "name": "Founder 1", "shares": 6000000 },
    { "name": "Founder 2", "shares": 4000000 }
  ],
  "safes": [
    { "name": "Y Combinator", "investment": 125000, "cap": 1785714, "discount": 0, "conversionType": "post" },
    { "name": "YC MFN", "investment": 375000, "cap": 0, "discount": 0, "conversionType": "post", "sideLetters": ["mfn"] }
  ],
  "seriesInvestors": [
    { "name": "Series A Lead", "investment": 4000000 }
  ],
  "targetOptionsPct": 0.10
}'
```

---

## Worked Example: "50/50, raised 1M on SAFEs at 10M caps, no round yet"

**Founder says:** "My co-founder and I are 50/50. We raised $1M on SAFEs at $10M caps. No priced round yet."

**Translation:**

| Phrase | Translation |
|--------|-------------|
| "50/50" | Two founders: 5M and 5M shares (10M total) |
| "$1M on SAFEs at $10M caps" | One or more SAFEs totaling $1M, each with $10M cap |
| "no round yet" | Use `estimated-pre-round` command |

**Clarifying questions:**

1. How many SAFEs and what amounts each? (If single: $1M at $10M)
2. Any discounts on the SAFEs? (Common: 20%, but ask)
3. Pre-money or post-money SAFEs? (Default: post)
4. Any MFN or uncapped SAFEs?
5. Existing option pool?

**CLI command (assuming single $1M post-money SAFE at $10M cap, 20% discount):**

```bash
npx @1984vc/cap-table@^0.2.1 estimated-pre-round '{
  "common": [
    { "name": "Founder 1", "shares": 5000000 },
    { "name": "Founder 2", "shares": 5000000 }
  ],
  "safes": [
    { "name": "Seed SAFE", "investment": 1000000, "cap": 10000000, "discount": 0.20, "conversionType": "post" }
  ]
}'
```

---

## Worked Example: "We did YC, then raised 2M on a 12M cap, looking at 5 on 25 pre"

**Founder says:** "We did YC, then raised $2M on SAFEs at a $12M cap. Now looking at a Series A -- $5M on $25M pre."

**Translation:**

| Phrase | Translation |
|--------|-------------|
| "did YC" | Two SAFEs: $125K @ $1.785M cap, $375K uncapped MFN |
| "$2M on a $12M cap" | $2M post-money SAFE at $12M cap (assume post, no discount unless stated) |
| "5 on 25 pre" | $5M Series A at $25M pre-money |
| (implied) | 10% option pool (Series A standard) |
| (implied) | Two founders -- ask for split |

**Clarifying questions:**

1. What's your founder split? (e.g., 50/50, 60/40)
2. How many total common shares?
3. Any discount on the $2M SAFE?
4. What's the lead investor's name?
5. Any other SAFEs or existing option pool?

**CLI command (assuming 50/50 split, no discount on seed SAFE):**

```bash
npx @1984vc/cap-table@^0.2.1 priced-round '{
  "preMoneyValuation": 25000000,
  "common": [
    { "name": "Founder 1", "shares": 5000000 },
    { "name": "Founder 2", "shares": 5000000 }
  ],
  "safes": [
    { "name": "Y Combinator", "investment": 125000, "cap": 1785714, "discount": 0, "conversionType": "post" },
    { "name": "YC MFN", "investment": 375000, "cap": 0, "discount": 0, "conversionType": "post", "sideLetters": ["mfn"] },
    { "name": "Seed SAFE", "investment": 2000000, "cap": 12000000, "discount": 0, "conversionType": "post" }
  ],
  "seriesInvestors": [
    { "name": "Series A Lead", "investment": 5000000 }
  ],
  "targetOptionsPct": 0.10
}'
```
