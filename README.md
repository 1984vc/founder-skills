# 1984 Founders Handbook

One agent skill from [1984 Ventures](https://1984.vc) for startup founders: practical guidance on company formation, fundraising, cap tables, co-founder dynamics, M&A, engineering, and taxes.

## Install

After the repository is renamed:

```bash
npx skills add 1984vc/1984-founders-handbook
```

The repository contains one skill: [`1984-founders-handbook`](skills/1984-founders-handbook/).

## What it covers

| Area | Guidance and tools |
|---|---|
| Company formation | Startup ideas, choosing and separating from co-founders, founder equity |
| Cap tables | Ownership math, SAFE conversion, priced rounds, dilution, option pools |
| Raising seed and Series A | SAFEs, side letters, decks, term mechanics, secondaries, down rounds |
| Engineering | Seed-stage practices, open source marketing, telemetry |
| Mergers and acquisitions | Sale process, legal preparation, structures, negotiated terms |
| Taxes | Qualified Small Business Stock (QSBS) |

## Cap-table modeling

The skill uses [`@1984vc/cap-table`](https://www.npmjs.com/package/@1984vc/cap-table) for concrete ownership and dilution calculations:

```bash
npx @1984vc/cap-table@^0.2.1 priced-round '{ "preMoneyValuation": 12000000, ... }'
```

It can also save and share editable cap-table worksheets through [startup-finance.1984.vc](https://startup-finance.1984.vc).

## Example prompts

- *“How does a post-money SAFE convert at Series A?”*
- *“Model our cap table after a $5M Series A and give me a link I can share.”*
- *“What should I know before my co-founder leaves?”*
- *“What’s the difference between a structured round and a down round?”*
- *“How do I sell secondaries as a founder?”*

## License

- Handbook articles: [CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0/) — free to share with attribution, no derivatives.
- Cap-table tooling and operational references: [MIT](https://opensource.org/licenses/MIT).