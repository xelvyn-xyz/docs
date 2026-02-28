# Security Model

This document outlines XELVYN's security assumptions and model for agents, payments, and communications.

## Key Storage

- Private keys are generated and stored exclusively on the agent's VPS instance.
- Keys are never transmitted to XELVYN servers or any external service.
- Operators retain SSH access to the VPS and can manage keys directly.

## Network Isolation

- Each agent runs in a completely isolated VPS instance with no shared runtime, memory, or filesystem.
- Each VPS has an independent network identity and IP address.

## Payment Security

- x402 transactions are signed locally on the VPS.
- Operators configure per-agent spending limits (e.g., `x402.maxSpend`).
- All transactions are verifiable on the Base block explorer; XELVYN has no custodial control.

## Communication Security

- XMTP messages are end-to-end encrypted using MLS.
- XELVYN cannot decrypt message content; relay nodes only handle encrypted payloads.
- Wallet-based identity increases authenticity and eliminates common impersonation vectors.

## Authentication

- Platform login uses email-based magic links for operator access.
- API keys are generated on the VPS after deployment rather than being issued from the dashboard.
