# Cap Table Calculation and Sharing

Use the local CLI for calculation and the hosted Startup Finance tools when the founder needs a persistent, editable link.

| Need | Use |
|---|---|
| Calculate existing ownership, SAFE conversion, dilution, or a priced round | `npx @1984vc/cap-table@^0.2.1` |
| Save and share a SAFE-only model | Hosted `estimate_pre_round` |
| Save and share a priced-round model | Hosted `calculate_cap_table` |
| Reload or update a worksheet | Hosted `read_worksheet` / `update_worksheet` |

## Local calculation

Choose a CLI command based on the financing stage:

- `existing` — issued shareholders only
- `estimated-pre-round` — SAFEs are outstanding but no priced round exists
- `pre-round` — ownership before a known priced round closes
- `priced-round` — fully diluted ownership after SAFE conversion, new investment, and option-pool refresh

CLI fields use decimal percentages: `targetOptionsPct: 0.10` and `discount: 0.20` mean 10% and 20%.

Read [cap-table-calculator.md](cap-table-calculator.md) for complete schemas and examples. Read [cap-table-common-terms.md](cap-table-common-terms.md) when translating founder shorthand such as “4 on 20 post,” “did YC,” or “10% pool.”

## Hosted save and share

The hosted endpoint is:

```text
POST https://startup-finance.1984.vc/mcp
Content-Type: application/json
```

It accepts JSON-RPC 2.0 without authentication or an initialization handshake. Both calculation tools save a worksheet and return a URL shaped like:

```text
https://startup-finance.1984.vc/#<worksheetId>-<editKey>
```

Hosted fields use whole-number percentages: `targetOptionsPool: 10` and `discount: 20` mean 10% and 20%.

Always give the founder the returned worksheet URL. Use the worksheet ID (the part before the dash) with `read_worksheet`; updating also requires the edit key.

Read [startup-finance-api.md](startup-finance-api.md) for complete request schemas, SAFE types, curl examples, and response handling. The live source of truth is [startup-finance.1984.vc/llms.txt](https://startup-finance.1984.vc/llms.txt).