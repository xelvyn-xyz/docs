# Skills Library

XELVYN provides a modular skill library distributed as `@xelvyn/skills`.

| Name | Description | Category | Complexity | AI Support |
|---|---|---:|---:|---|
| yield-rebalancer | Automated DeFi rebalancing and optimizer | DeFi | Advanced | OpenAI, Claude |
| risk-monitor | Continuous risk monitoring and alerts | Security | Intermediate | OpenAI, Claude |
| gas-optimizer | Transaction gas optimization and batching | Infra | Basic | None |
| price-oracle | On-chain price aggregation and normalization | Data | Basic | None |
| smart-router | Advanced routing for multi-hop swaps | DeFi | Advanced | OpenAI, Claude |
| wallet-guard | Wallet anomaly detection and response | Security | Intermediate | Claude |
| portfolio-tracker | Aggregates positions and P&L across sources | Data | Basic | None |
| auto-compound | Periodic compounding for yield strategies | DeFi | Intermediate | OpenAI |
| sentiment-scanner | Market sentiment analysis from web sources | Data | Advanced | OpenAI, Claude (required) |

## Installation

```bash
xelvyn skill install <name> [--ai openai|claude]
```

AI integration is opt-in per skill.

- `OpenAI GPT-4o` for quantitative analysis, prediction, and sentiment scoring.
- `Claude` for reasoning, security analysis, and risk assessment.

Without AI, skills run deterministic rule-based logic.

## Programmatic Usage

```ts
import { listSkills, getSkill, getSkillsByCategory, getAIEnabledSkills } from '@xelvyn/skills'

const all = await listSkills()
const defi = getSkillsByCategory('DeFi')
```
