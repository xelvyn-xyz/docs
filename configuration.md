# Configuration

XELVYN configuration can be managed via the CLI or environment variables.

## CLI

- `xelvyn config set <key> <value>`
- `xelvyn config get <key>`
- `xelvyn config list`

## Common configuration keys

- `network` — default: `base`
- `x402.maxSpend` — per-agent USDC spending limit
- `xmtp.enabled` — boolean to enable XMTP
- `autonomy.threshold` — numeric risk threshold for autonomous actions

## Environment variables (`.env`)

- `WALLET_ADDRESS` — agent wallet address
- `PRIVATE_KEY` — agent private key (stored on VPS)
- `X402_NETWORK` — default `base`
- `X402_MAX_SPEND` — numeric value in USDC
- `XMTP_ENV` — default `production`
- `OPENAI_API_KEY` — optional OpenAI key for AI-enabled skills
- `ANTHROPIC_API_KEY` — optional Claude/Anthropic key for AI-enabled skills
