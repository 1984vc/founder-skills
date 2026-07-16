# Startup Finance Worksheet API

> Save, share, read, and update interactive cap table worksheets at [startup-finance.1984.vc](https://startup-finance.1984.vc).
>
> Canonical live docs: [https://startup-finance.1984.vc/llms.txt](https://startup-finance.1984.vc/llms.txt)
>
> For local CLI ownership math, see the parent `SKILL.md`. Use **this** reference when the founder wants a shareable link or editable web worksheet.

Interactive worksheet: https://startup-finance.1984.vc

## When to use (from the skill)

| Situation | Tool |
|-----------|------|
| SAFE-only / no priced round; save & share | `estimate_pre_round` |
| Priced round (Series A/B, pool, series) | `calculate_cap_table` |
| Reload a shared worksheet | `read_worksheet` |
| Change a previously saved worksheet | `update_worksheet` |

Both `estimate_pre_round` and `calculate_cap_table` **save a shareable worksheet and return a link**. Give the founder that URL after modeling.

## CLI → API field mapping

| CLI (`@1984vc/cap-table`) | Hosted API | Notes |
|--------------------------|------------|-------|
| `common[]` (shareholders) | `shareholders[]` | `{ name, shares }` |
| `common[]` with `commonType: "unusedOptions"` | `unusedOptions` | Number (total unused option shares) |
| `safes[].discount` as `0.20` | `safes[].discount` as `20` | CLI = decimal; API = whole % |
| `targetOptionsPct` as `0.10` | `targetOptionsPool` as `10` | CLI = decimal; API = whole % |
| `seriesInvestors[]` | `seriesInvestment[]` | `{ name, investment }` |
| `conversionType` + `sideLetters` | `safes[].type` | `post` / `pre` / `mfn` / `yc7p` / `ycmfn` |

---

# Startup Finance Cap Table Calculator (API docs)

> Model startup funding rounds, SAFE conversions, and cap tables via MCP or plain HTTP.

Interactive worksheet: https://startup-finance.1984.vc

## MCP Endpoint

All tools are available via a single JSON-RPC 2.0 endpoint:

```
POST https://startup-finance.1984.vc/mcp
Content-Type: application/json
```

No authentication required. No session handshake needed — skip `initialize` and call tools directly.

### Available Tools

| Tool | Use When |
|------|----------|
| `estimate_pre_round` | SAFE-only, no priced round yet — shows ownership assuming all SAFEs convert at their cap |
| `calculate_cap_table` | Modeling a priced round (Series A/B/etc.) with SAFEs converting |
| `read_worksheet` | Read a previously saved worksheet by ID |
| `update_worksheet` | Update a saved worksheet with new inputs |

Both `estimate_pre_round` and `calculate_cap_table` save a shareable worksheet and return a link.

---

## Tool: estimate_pre_round

Estimates cap table ownership before any priced round. Each SAFE converts at its own cap. Use this for early-stage companies with SAFE notes outstanding and no Series A yet.

### Request

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/call",
  "params": {
    "name": "estimate_pre_round",
    "arguments": {
      "name": "Acme Pre-Seed",
      "shareholders": [
        { "name": "Founder 1", "shares": 5000000 },
        { "name": "Founder 2", "shares": 5000000 }
      ],
      "unusedOptions": 500000,
      "safes": [
        { "name": "YC", "investment": 125000, "cap": 1785715, "discount": 0, "type": "yc7p" },
        { "name": "Angel MFN", "investment": 250000, "cap": 0, "discount": 0, "type": "mfn" },
        { "name": "Seed Fund", "investment": 500000, "cap": 10000000, "discount": 0, "type": "post" }
      ]
    }
  }
}
```

### Example: YC company curl

```bash
curl -X POST https://startup-finance.1984.vc/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "estimate_pre_round",
      "arguments": {
        "name": "Acme YC S24",
        "shareholders": [
          { "name": "Alice (CEO)", "shares": 5000000 },
          { "name": "Bob (CTO)", "shares": 4000000 }
        ],
        "unusedOptions": 1000000,
        "safes": [
          { "name": "YC", "investment": 125000, "cap": 1785715, "discount": 0, "type": "yc7p" },
          { "name": "YC MFN", "investment": 375000, "cap": 0, "discount": 0, "type": "ycmfn" },
          { "name": "1984 Ventures", "investment": 750000, "cap": 10000000, "discount": 0, "type": "post" },
          { "name": "Angel", "investment": 250000, "cap": 8000000, "discount": 0, "type": "post" }
        ]
      }
    }
  }'
```

### Example: Simple seed with SAFEs only

```bash
curl -X POST https://startup-finance.1984.vc/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "estimate_pre_round",
      "arguments": {
        "shareholders": [
          { "name": "Founder", "shares": 10000000 }
        ],
        "unusedOptions": 1000000,
        "safes": [
          { "name": "Pre-seed Fund", "investment": 500000, "cap": 8000000, "discount": 0, "type": "post" },
          { "name": "Angel", "investment": 200000, "cap": 6000000, "discount": 20, "type": "post" }
        ]
      }
    }
  }'
```

---

## Tool: calculate_cap_table

Calculates a full priced round cap table. SAFEs convert at the round price (capped by their cap/discount). Returns PPS, ownership percentages, dilution, and a shareable worksheet link.

### Example: Series A with SAFE conversion

```bash
curl -X POST https://startup-finance.1984.vc/mcp \
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
        "unusedOptions": 500000,
        "safes": [
          { "name": "YC", "investment": 125000, "cap": 1785715, "discount": 0, "type": "yc7p" },
          { "name": "YC MFN", "investment": 375000, "cap": 0, "discount": 0, "type": "ycmfn" },
          { "name": "1984 Ventures", "investment": 750000, "cap": 10000000, "discount": 0, "type": "post" }
        ],
        "seriesInvestment": [
          { "name": "Benchmark", "investment": 5000000 },
          { "name": "Angel Syndicate", "investment": 1000000 }
        ]
      }
    }
  }'
```

### Example: Clean Series A (no SAFEs)

```bash
curl -X POST https://startup-finance.1984.vc/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "calculate_cap_table",
      "arguments": {
        "preMoneyValuation": 25000000,
        "targetOptionsPool": 10,
        "shareholders": [
          { "name": "Founder 1", "shares": 5000000 },
          { "name": "Founder 2", "shares": 5000000 }
        ],
        "seriesInvestment": [
          { "name": "Lead VC", "investment": 5000000 }
        ]
      }
    }
  }'
```

### Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| name | string | No | Worksheet name |
| preMoneyValuation | number | Yes | Pre-money valuation in dollars |
| targetOptionsPool | number | Yes | Target options pool as whole percentage (e.g. 10 for 10%) |
| shareholders | array | Yes | Common stockholders with name and shares |
| unusedOptions | number | No | Existing unused options (default: 0) |
| safes | array | No | SAFE notes — see SAFE Types below |
| seriesInvestment | array | No | New round investors with name and investment |

---

## Tool: read_worksheet

Reads a saved worksheet by ID and returns its inputs plus recalculated results.

```bash
curl -X POST https://startup-finance.1984.vc/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "read_worksheet",
      "arguments": {
        "worksheetId": "ZRmCcrJMU4izzuVc3"
      }
    }
  }'
```

The `worksheetId` is the part before the dash in the worksheet URL hash, e.g. `ZRmCcrJMU4izzuVc3` from `https://startup-finance.1984.vc/#ZRmCcrJMU4izzuVc3-SUeN7a`.

---

## Tool: update_worksheet

Updates an existing worksheet. Requires the worksheet ID and edit key (the part after the dash in the URL hash).

```bash
curl -X POST https://startup-finance.1984.vc/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
      "name": "update_worksheet",
      "arguments": {
        "worksheetId": "ZRmCcrJMU4izzuVc3",
        "editKey": "SUeN7a",
        "preMoneyValuation": 22000000,
        "targetOptionsPool": 10,
        "shareholders": [
          { "name": "Alice (CEO)", "shares": 5000000 },
          { "name": "Bob (CTO)", "shares": 4000000 }
        ],
        "safes": [
          { "name": "YC", "investment": 125000, "cap": 1785715, "discount": 0, "type": "yc7p" }
        ],
        "seriesInvestment": [
          { "name": "Lead VC", "investment": 5000000 }
        ]
      }
    }
  }'
```

---

## SAFE Types

| Type | Description |
|------|-------------|
| `post` | Post-money SAFE — ownership% = investment / cap |
| `pre` | Pre-money SAFE — shares = (investment / cap) × pre-money shares |
| `mfn` | MFN SAFE — uncapped; cap auto-assigned to the lowest cap in subsequent SAFEs. Set `cap: 0` |
| `ycmfn` | YC MFN SAFE — same mechanics as `mfn`. Set `cap: 0` |
| `yc7p` | YC 7% SAFE — gives exactly 7% post-money. Set `cap = investment / 0.07` (e.g. `1785715` for $125K) |

### Notes

- All monetary values are in dollars (not cents)
- Percentages are whole numbers (10 for 10%, not 0.10)
- Discount is a whole percentage (20 for 20% discount)
- For `mfn` and `ycmfn`, order matters — the MFN SAFE gets the lowest cap of all SAFEs listed after it
- `estimate_pre_round` shows ownership assuming conversion at cap; discounts are noted as caveats since they cannot be applied without a priced round

---

## Sharing workflow

1. Call `estimate_pre_round` or `calculate_cap_table` with the modeled scenario.
2. Parse the response for the worksheet URL (typically a `worksheetUrl` field and/or text like `View and edit this cap table at: <url>`).
3. Give the founder that URL — it opens an interactive worksheet pre-loaded with their numbers.
4. URL shape: `https://startup-finance.1984.vc/#<worksheetId>-<editKey>`
   - Full hash (with edit key) lets them re-edit and re-save.
   - Use `read_worksheet` later with `worksheetId` (part before the last dash) to pull their edits back into a conversation.

Always share the worksheet URL after saving when the founder may reopen or tweak the model later.