# Getting Started

This guide walks through deploying your first XELVYN agent.

## Prerequisites

- Node.js 20+
- `npm`

## Step 1 — Install CLI

```bash
npm install -g @xelvyn/cli
```

## Step 2 — Login

```bash
xelvyn login
```

## Step 3 — Initialize an agent

```bash
xelvyn init my-agent --template yield --network base
```

Available templates: `yield`, `monitor`, `router`, `custom`.

## Step 4 — Configure environment

Edit `.env` and add:

```
WALLET_ADDRESS=0x...
PRIVATE_KEY=0x...
```

## Step 5 — Install skills

```bash
xelvyn skill install yield-rebalancer --ai openai
```

## Step 6 — Deploy

```bash
xelvyn deploy --x402 --xmtp
```

Use `--dry-run` for a simulation.

## Step 7 — Monitor

```bash
xelvyn status my-agent --live
```
