# 1984vc Founder Skills

A collection of [skills](https://www.npmjs.com/package/skills) from [1984vc](https://1984.vc) — practical guides and tools for startup founders covering fundraising mechanics, cap table math, co-founder dynamics, M&A, engineering, and taxes.

## Install

```bash
npx skills add 1984vc/founder-skills
```

## Skills

| Skill | Description |
|-------|-------------|
| **[founders-handbook](skills/founders-handbook/)** | The [1984vc Founders Handbook](https://1984.vc/docs/founders-handbook) — 22 guides across company formation, fundraising, equity mechanics, M&A, engineering, and taxes. |
| **[cap-table](skills/cap-table/)** | Model startup cap table ownership — SAFE conversions, priced rounds, option pool refreshes, and dilution. Powered by [`@1984vc/cap-table`](https://github.com/1984vc/cap-table). |

### founders-handbook

A reference library of practical guides for startup founders. Example prompts:

- *"How does a post-money SAFE convert at Series A?"*
- *"What should I know before my co-founder leaves?"*
- *"Walk me through the cap table impact of raising a Series A with a 10% option pool."*
- *"What's the difference between a structured round and a downround?"*
- *"How do I sell secondaries as a founder?"*

Guides cover six topic areas:

| Category | Guides |
|---|---|
| Company Formation | Cap table math, picking a startup idea, choosing / departing co-founders, minimizing dilution |
| Raising Your Seed | SAFEs, pre/post-money conversion, SAFE vs priced rounds, side letters |
| Raising Your A | Series A deck, cap table impact, selling secondaries, structured/down rounds |
| Engineering | Seed-stage best practices, open source content marketing, telemetry |
| Mergers & Acquisitions | How to sell, legal prep, deal structure, key terms |
| Taxes | QSBS ($15M federal exclusion) |

### cap-table

An interactive cap table calculator. Commands:

| Command | Use case |
|---------|----------|
| `existing` | Just existing shareholders, no SAFEs or rounds |
| `estimated-pre-round` | Have SAFEs but no priced round — estimates ownership |
| `pre-round` | Know the round valuation — shows pre-money ownership |
| `priced-round` | Full round with SAFE conversions, series investors, option pool |

```bash
npx @1984vc/cap-table priced-round '{ "preMoneyValuation": 12000000, ... }'
```

## About

Written by the partners at [1984vc](https://1984.vc).

## License

- **founders-handbook**: [![License: CC BY-ND 4.0](https://licensebuttons.net/l/by-nd/4.0/88x31.png)](https://creativecommons.org/licenses/by-nd/4.0/) — Free to share with attribution, no derivatives.
- **cap-table**: [MIT](https://opensource.org/licenses/MIT) — [1984 Ventures](https://1984.vc)
