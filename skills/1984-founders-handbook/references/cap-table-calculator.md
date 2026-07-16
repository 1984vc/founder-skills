# Cap Table Calculator

> Model startup cap tables: ownership percentages, SAFE conversions, priced rounds, and option pool refreshes. Save and share interactive worksheets at [startup-finance.1984.vc](https://startup-finance.1984.vc).

This is the detailed calculator reference for the unified `1984-founders-handbook` skill. Run the CLI as `npx @1984vc/cap-table@^0.2.1`; version 0.2.1 or later correctly applies MFN side letters during priced-round conversion.

## Founder Shorthand

Founders describe their cap table in shorthand. Translate to CLI inputs:

| Phrase | Meaning | CLI mapping |
|--------|---------|-------------|
| "60/40" | Two founders splitting 60%/40% | `common: [{shares: 6000000}, {shares: 4000000}]` (assume 10M total) |
| "did YC" / "went through YC" | YC's $500K standard deal | Two SAFEs — see below |
| "4 on 20 post" | $4M raise at $20M post-money | `preMoneyValuation: 16000000` (post − raise) |
| "4 on 20 pre" | $4M raise at $20M pre-money | `preMoneyValuation: 20000000` |
| "10% pool" | Option pool target | `targetOptionsPct: 0.10` |
| "20% discount" | SAFE discount | `discount: 0.20` |
| "uncapped" / "MFN" | No cap, MFN side letter | `cap: 0, sideLetters: ["mfn"]` |
| "no round yet" | SAFEs only, no priced round | Use `estimated-pre-round` command |

### YC Standard Deal

YC invests $500K via two post-money SAFEs — always model both, in this order, before other investors:

```json
{ "name": "Y Combinator", "investment": 125000, "cap": 1785714, "discount": 0, "conversionType": "post" },
{ "name": "YC MFN", "investment": 375000, "cap": 0, "discount": 0, "conversionType": "post", "sideLetters": ["mfn"] }
```

- **$125K at $1,785,714 cap** = exactly 7% equity (125,000 / 1,785,714 = 0.07)
- **$375K uncapped MFN** = adopts lowest cap from subsequent SAFEs; converts at round price if none

### Common Defaults

| What | Default | Notes |
|------|---------|-------|
| `conversionType` | `"post"` | Post-money is the YC standard since 2018 |
| `targetOptionsPct` | `0.10` | 10% pool is standard for Series A |
| `discount` | `0` | 20% (0.20) common for capped seed SAFEs |
| Founder shares | 10,000,000 total | Common starting point; only ratio matters |

For the full glossary, typical terms by stage, and worked examples, see [`cap-table-common-terms.md`](cap-table-common-terms.md).

## Commands

| Command | When to use |
|---------|-------------|
| `existing` | Just existing shareholders, no SAFEs or rounds |
| `estimated-pre-round` | Have SAFEs but no priced round yet — estimates ownership |
| `pre-round` | Know the priced round valuation — shows pre-money ownership |
| `priced-round` | Full priced round with SAFE conversions, series investors, option pool |

## Input Format

All commands accept a JSON object. You can pass it as an argument, pipe via stdin, or point to a `.json` file.

```bash
# As argument
npx @1984vc/cap-table@^0.2.1 priced-round '{...}'

# Via stdin
echo '{...}' | npx @1984vc/cap-table@^0.2.1 priced-round

# From file
npx @1984vc/cap-table@^0.2.1 priced-round ./input.json
```

### Input Schema

```json
{
  "preMoneyValuation": 12000000,
  "common": [
    { "name": "Founder 1", "shares": 4500000 },
    { "name": "Founder 2", "shares": 4500000 },
    { "name": "Options Pool", "shares": 1000000, "commonType": "unusedOptions" }
  ],
  "safes": [
    {
      "name": "Seed SAFE",
      "investment": 1000000,
      "cap": 10000000,
      "discount": 0,
      "conversionType": "post"
    }
  ],
  "seriesInvestors": [
    { "name": "Lead Investor", "investment": 2000000 }
  ],
  "targetOptionsPct": 0.10
}
```

**Fields:**

| Field | Required | Default | Description |
|-------|----------|---------|-------------|
| `preMoneyValuation` | priced-round, pre-round | — | Pre-money valuation in dollars |
| `common[].name` | yes | — | Shareholder name |
| `common[].shares` | yes | — | Number of shares |
| `common[].commonType` | no | `"shareholder"` | Use `"unusedOptions"` for unissued option pool |
| `safes[].investment` | yes | — | Dollar amount invested |
| `safes[].cap` | no | `0` | Valuation cap (0 = uncapped) |
| `safes[].discount` | no | `0` | Discount as decimal (0.2 = 20%) |
| `safes[].conversionType` | no | `"post"` | `"pre"` or `"post"` money conversion |
| `safes[].sideLetters` | no | — | Array: `["mfn"]` for Most Favored Nation |
| `seriesInvestors[].investment` | yes | — | Dollar amount invested |
| `targetOptionsPct` | no | `0.10` | Target option pool % post-round |
| `unusedOptions` | no | auto-detected | Explicit unused options count |

**Note:** You do NOT need to pass `type: "common"`, `type: "safe"`, etc. The CLI auto-fills these.

### For `existing` only:

```json
{
  "common": [
    { "name": "Founder 1", "shares": 8000000 },
    { "name": "Founder 2", "shares": 2000000 }
  ]
}
```

## Output

### `existing` → Array of rows

```json
[
  { "name": "Founder 1", "shares": 8000000, "ownershipPct": 0.8, "type": "common" },
  { "name": "Founder 2", "shares": 2000000, "ownershipPct": 0.2, "type": "common" }
]
```

### `estimated-pre-round` → Object

```json
{
  "common": [...],
  "safes": [...],
  "total": { "name": "Total", "shares": 10666666, "investment": 500000, "ownershipPct": 1 }
}
```

### `priced-round` / `pre-round` → Object with conversion + capTable

```json
{
  "conversion": {
    "pps": 1.04836,
    "ppss": [0.90001],
    "totalShares": 13354265,
    "newSharesIssued": 3354265,
    "preMoneyShares": 10335426,
    "postMoneyShares": 11111098,
    "convertedSafeShares": 1111098,
    "seriesShares": 1907741,
    "additionalOptions": 335426,
    "totalOptions": 1335426,
    "totalInvested": 3000000
  },
  "capTable": {
    "common": [...],
    "safes": [
      { "name": "Seed SAFE", "investment": 1000000, "ownershipPct": 0.083, "shares": 1111098, "pps": 0.90001 }
    ],
    "series": [
      { "name": "Lead", "investment": 2000000, "ownershipPct": 0.143, "shares": 1907741, "pps": 1.04836 }
    ],
    "refreshedOptionsPool": { "shares": 1335426, "ownershipPct": 0.1 },
    "total": { "shares": 13354265, "investment": 3000000, "ownershipPct": 1 }
  }
}
```

## Key Concepts

### SAFE Conversion

SAFEs convert to equity at a priced round. The investor gets the **better** of two prices:

- **Cap price**: `cap / shares` (guarantees minimum ownership %)
- **Discount price**: `(1 - discount) * seriesPPS` (discount off round price)

**Pre-money SAFEs** convert on the pre-money share count. **Post-money SAFEs** (YC standard) guarantee a fixed ownership % post-money.

### MFN (Most Favored Nation)

An MFN SAFE has no explicit cap but gets the lowest cap from subsequent capped SAFEs. Pass `sideLetters: ["mfn"]`.

### Option Pool Refresh

`targetOptionsPct` controls the post-round option pool size (common: 10-20%). The gap between current unissued pool and target creates additional dilution shared by existing shareholders.

### Ownership Percentages

All `ownershipPct` values are decimals: `0.45` = 45%. The solver iteratively converges on self-consistent share counts.

## Quick Examples

```bash
# Simple existing ownership
npx @1984vc/cap-table@^0.2.1 existing '{
  "common": [
    {"name": "Alice", "shares": 6000000},
    {"name": "Bob", "shares": 4000000}
  ]
}'

# Pre-round with SAFEs (no priced round)
npx @1984vc/cap-table@^0.2.1 estimated-pre-round '{
  "common": [
    {"name": "Founder", "shares": 8000000},
    {"name": "Pool", "shares": 2000000, "commonType": "unusedOptions"}
  ],
  "safes": [
    {"name": "Angel 1", "investment": 250000, "cap": 5000000},
    {"name": "Angel 2", "investment": 500000, "cap": 8000000}
  ]
}'

# Full Series A
npx @1984vc/cap-table@^0.2.1 priced-round '{
  "preMoneyValuation": 20000000,
  "common": [
    {"name": "CEO", "shares": 4000000},
    {"name": "CTO", "shares": 4000000},
    {"name": "Pool", "shares": 500000},
    {"name": "Unissued", "shares": 500000, "commonType": "unusedOptions"}
  ],
  "safes": [
    {"name": "Seed Fund", "investment": 1500000, "cap": 8000000}
  ],
  "seriesInvestors": [
    {"name": "Series A Lead", "investment": 5000000}
  ],
  "targetOptionsPct": 0.15
}'
```

## Error Handling

Invalid input (e.g., SAFE investment >= cap) exits with non-zero code and error to stderr. Always check the exit code.

## Save & share worksheets

The CLI calculates more ownership math, but it does **not** persist a link. Founders can **save and share** interactive cap tables on [startup-finance.1984.vc](https://startup-finance.1984.vc) — a browser worksheet plus a free HTTP/MCP API that returns a shareable URL.

### When to use it

Do this after you've modeled a scenario (or when the founder asks for a link / something they can edit with a co-founder or investor):

| Situation | Action |
|-----------|--------|
| Founder wants a **shareable link** | Call the hosted API; return the worksheet URL |
| Founder wants an **interactive what-if UI** | Same — worksheet opens at https://startup-finance.1984.vc |
| SAFE-only / pre-priced round | Hosted tool: `estimate_pre_round` |
| Priced round (Series A/B, pool, series) | Hosted tool: `calculate_cap_table` |
| Resume a prior shared sheet | Hosted tool: `read_worksheet` / `update_worksheet` |

Both `estimate_pre_round` and `calculate_cap_table` **automatically save** a worksheet and return a shareable link. Prefer giving that link whenever you hand off results the founder might reopen later.

### How (high level)

1. Map the same numbers you used for the CLI into the hosted tool payload (see field mapping in the reference).
2. `POST` JSON-RPC to `https://startup-finance.1984.vc/mcp` — no auth, no session handshake.
3. Extract the worksheet URL from the response and share it with the founder.
4. URLs look like `https://startup-finance.1984.vc/#<worksheetId>-<editKey>`.

Quick save (priced round sketch — full request shapes and SAFE types in the reference):

```bash
curl -s -X POST https://startup-finance.1984.vc/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "calculate_cap_table",
      "arguments": {
        "name": "Acme Series A",
        "preMoneyValuation": 20000000,
        "targetOptionsPool": 10,
        "shareholders": [
          { "name": "Alice (CEO)", "shares": 5000000 },
          { "name": "Bob (CTO)", "shares": 4000000 }
        ],
        "seriesInvestment": [
          { "name": "Lead VC", "investment": 5000000 }
        ]
      }
    }
  }'
```

**Gotchas vs the CLI:** hosted API uses **whole-number** percentages and discounts (`10` for 10%, `20` for 20% discount), not decimals (`0.10` / `0.20`). SAFE typing uses `type` (`post`, `pre`, `mfn`, `yc7p`, `ycmfn`) instead of `conversionType` + `sideLetters`.

Full endpoints, field mapping from CLI → API, YC examples, `read_worksheet` / `update_worksheet`, and response handling: [`startup-finance-api.md`](startup-finance-api.md). Live machine-readable docs: [https://startup-finance.1984.vc/llms.txt](https://startup-finance.1984.vc/llms.txt).

## Advanced

For programmatic TypeScript/JavaScript use: `npm install @1984vc/cap-table`. See [`cap-table-library-api.md`](cap-table-library-api.md) for the full interface, math foundations, and type reference.

- Worksheet UI / share: https://startup-finance.1984.vc
- Worksheet API reference: [`startup-finance-api.md`](startup-finance-api.md)
- GitHub: https://github.com/1984vc/cap-table
- npm: https://www.npmjs.com/package/@1984vc/cap-table
