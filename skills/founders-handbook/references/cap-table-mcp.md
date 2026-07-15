# Cap Table MCP

*Source: [startup-finance.1984.vc](https://startup-finance.1984.vc/)*

Live cap table calculations via the 1984 Ventures MCP at `https://startup-finance.1984.vc/mcp`.

**Tools:** `calculate_cap_table`, `read_worksheet`, `update_worksheet`

Returns share counts, ownership percentages, price per share, a summary with total investment raised and founder dilution, and a `worksheetUrl` the founder can open and edit interactively.

---

## Two modes

**SAFE-only (default for early-stage founders)**  
Most founders asking about their cap table are pre-Series A. The SAFEs haven't converted yet — there's no priced round. To model ownership, pick a hypothetical conversion valuation (or use the current post-money cap of the largest SAFE as a proxy). Set `targetOptionsPool: 0` and leave `seriesInvestment` empty. This shows what everyone would own if the SAFEs converted today at that valuation, without the dilution of a new options pool.

**Full priced round (optional)**  
When the founder wants to see a specific Series A scenario, set `targetOptionsPool` (10% is standard) and populate `seriesInvestment` with the new investors. This models the complete picture at close.

---

## Input Schema

```json
{
  "name": "optional worksheet name",  // e.g. "Acme Seed Round"
  "preMoneyValuation": 8000000,       // hypothetical conversion valuation (required)
  "targetOptionsPool": 0,             // 0 for SAFE-only; 10 for a real priced round
  "shareholders": [                   // existing common stock (required)
    { "name": "string", "shares": 5000000 }
  ],
  "unusedOptions": 0,                 // existing unissued options (default: 0)
  "safes": [                          // SAFEs converting at this valuation (default: [])
    {
      "name": "string",
      "investment": 125000,           // dollars
      "cap": 1785714,                 // valuation cap (0 = uncapped)
      "discount": 0,                  // e.g. 20 for 20% discount, 0 for none
      "type": "post"                  // "pre" | "post"
    }
  ],
  "seriesInvestment": [               // new priced-round investors — omit for SAFE-only
    { "name": "string", "investment": 500000 }
  ]
}
```

### YC standard deal (current)

Always model YC as two separate SAFEs in this order, before any other investors:

1. **$125,000 post-money SAFE at $1,785,714 cap** — gives YC exactly 7% at conversion (when `targetOptionsPool: 0`)
2. **$375,000 post-money SAFE, uncapped (`cap: 0`)** — the MFN tranche; converts at the round price

```json
{ "name": "Y Combinator", "investment": 125000, "cap": 1785714, "discount": 0, "type": "post" },
{ "name": "YC MFN",       "investment": 375000, "cap": 0,       "discount": 0, "type": "post" }
```

Other SAFE investors follow after these two entries.

> **Note:** Setting `targetOptionsPool` > 0 will dilute YC's post-money SAFE below 7% because the options pool is created before SAFE conversion in the MCP's calculation order. For pure SAFE modeling, always use `targetOptionsPool: 0`.

---

## Example: YC + Seed Investor (SAFE-only)

**Scenario:** Two co-founders, YC on their standard deal ($125K capped + $375K MFN), and a seed investor with $500K at an $8M cap. Modeling ownership at a hypothetical $8M pre-money conversion — no priced round, no options pool.

### Request

```json
{
  "name": "SAFE-only snapshot",
  "preMoneyValuation": 8000000,
  "targetOptionsPool": 0,
  "shareholders": [
    { "name": "Alice (CEO)", "shares": 5000000 },
    { "name": "Bob (CTO)",   "shares": 5000000 }
  ],
  "safes": [
    { "name": "Y Combinator",  "investment": 125000, "cap": 1785714, "discount": 0, "type": "post" },
    { "name": "YC MFN",        "investment": 375000, "cap": 0,       "discount": 0, "type": "post" },
    { "name": "Seed Investor", "investment": 500000, "cap": 8000000, "discount": 0, "type": "post" }
  ],
  "seriesInvestment": []
}
```

### Result

| Stakeholder    | Shares      | Ownership | Notes                                      |
|----------------|-------------|-----------|--------------------------------------------|
| Alice (CEO)    | 5,000,000   | 41.03%    | Common                                     |
| Bob (CTO)      | 5,000,000   | 41.03%    | Common                                     |
| Y Combinator   | 852,951     | 7.00%     | SAFE converts at $0.147/sh (capped)        |
| YC MFN         | 571,202     | 4.69%     | Uncapped — converts at round price         |
| Seed Investor  | 761,603     | 6.25%     | SAFE converts at round price ($0.657/sh)   |
| **Total**      | **12,185,756** | **100%** |                                           |

**Price per share:** $0.6565  
**Total raised:** $1,000,000  
**Founder dilution:** 17.94%

YC's capped SAFE converts at a much lower price ($0.147/sh) than the round because their $1.785M cap is well below the $8M pre-money. The MFN and seed investor both convert at the round price.

Always share the `worksheetUrl` with the founder — it opens an interactive worksheet pre-loaded with their scenario so they can adjust the hypothetical valuation and explore what-ifs.

---

## Adding a priced round

To model a full Series A on top of the SAFE stack, add `targetOptionsPool` and `seriesInvestment`:

```json
{
  "preMoneyValuation": 10000000,
  "targetOptionsPool": 10,
  "shareholders": [ ... same founders ... ],
  "safes": [ ... same SAFEs ... ],
  "seriesInvestment": [
    { "name": "Lead VC", "investment": 3000000 }
  ]
}
```

This shows the fully diluted cap table after the round closes, including the options pool refresh.

---

## Reading a worksheet back

After sharing a `worksheetUrl` with a founder, use `read_worksheet` to see any edits they've made:

```json
{ "name": "read_worksheet", "arguments": { "worksheetId": "nudG2B9NKoLyF2sC3" } }
```

The `worksheetId` is the part of the URL hash **before the last dash**: from `https://startup-finance.1984.vc/#nudG2B9NKoLyF2sC3-Wo22bH`, the ID is `nudG2B9NKoLyF2sC3`.

Returns the stored inputs plus a fresh recalculation — useful for resuming a conversation after the founder has adjusted their numbers.

---

## How to Call It

Use `curl` — it's the simplest path and works in any context. The server speaks JSON-RPC 2.0 over HTTPS POST.

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
        "preMoneyValuation": 8000000,
        "targetOptionsPool": 0,
        "shareholders": [
          { "name": "Alice (CEO)", "shares": 5000000 },
          { "name": "Bob (CTO)",   "shares": 5000000 }
        ],
        "safes": [
          { "name": "Y Combinator",  "investment": 125000, "cap": 1785714, "discount": 0, "type": "post" },
          { "name": "YC MFN",        "investment": 375000, "cap": 0,       "discount": 0, "type": "post" },
          { "name": "Seed Investor", "investment": 500000, "cap": 8000000, "discount": 0, "type": "post" }
        ],
        "seriesInvestment": []
      }
    }
  }'
```

The response is a JSON-RPC envelope with two content items:

- `result.content[0].text` — JSON string containing the full cap table, summary metrics, and a `worksheetUrl`
- `result.content[1].text` — plain text: `"View and edit this cap table at: <url>"`

Extract the cap table and worksheet URL:

```bash
curl -s -X POST https://startup-finance.1984.vc/mcp \
  -H "Content-Type: application/json" \
  -d '{ ... }' | python3 -c "
import sys, json
envelope = json.load(sys.stdin)
data = json.loads(envelope['result']['content'][0]['text'])
for row in data['result']['capTable']:
    print(f\"{row['name']:20} {row['ownershipPercent']:.2f}%\")
print()
print('Worksheet:', data['worksheetUrl'])
"
```

The server is also a valid MCP endpoint (JSON-RPC 2.0, `tools/list` and `tools/call` methods) so it can be added to Claude Code as an MCP server if preferred, but curl is the straightforward default.
