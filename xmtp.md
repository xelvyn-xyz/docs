# XMTP Messaging

XMTP (Extensible Message Transport Protocol) is a decentralized end-to-end encrypted messaging protocol used by XELVYN for operator-agent communication.

## Why XMTP

- Wallet-based identity: no phone numbers or emails required.
- End-to-end encryption: MLS-based Message Layer Security.
- Decentralized relays: no single point of failure.
- Persistent history: accessible from any authorized client.

Agents use the same wallet identity for XMTP and x402, producing a unified cryptographic identity.

## Agent-to-Operator Flow

- Deploying with `--xmtp` initializes an XMTP identity on the VPS.
- Agents send deployment confirmations, execution reports, x402 receipts, and error alerts.
- Operators can send commands such as pause, resume, or reconfigure.

## Message Types

1. `DEPLOY` — deployment confirmation
2. `ALERT` — threshold breach or warning
3. `REPORT` — execution summary
4. `COMMAND` — operator instruction (pause/resume/config)
5. `ERROR` — error notification

## Message Structure

```json
{
  "type": "REPORT",
  "timestamp": "2026-02-28T12:00:00Z",
  "agentId": "my-agent",
  "payload": { "summary": "Rebalance completed", "details": {...} }
}
```

All timestamps are in UTC.

## CLI

- `xelvyn xmtp read` — read messages for an agent from the operator's console.

## SDK

- `client.xmtp.send(agentName, message)` — send a message
- `client.xmtp.messages(agentName)` — list messages

## Privacy Guarantees

- Messages are encrypted before leaving the VPS; relay nodes cannot read content.
- XELVYN does not store or have access to decrypted content.
- Private keys for XMTP signing are stored exclusively on the VPS.
