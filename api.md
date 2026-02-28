# REST API Reference

Base URL: `https://api.xelvyn.xyz/v1`

Authentication: Bearer token in `Authorization` header.

Example header:

```
Authorization: Bearer <API_KEY>
Content-Type: application/json
```

## Endpoints

### POST /agents/deploy

Request

```json
{ "name": "my-agent", "template": "yield", "network": "base", "x402": true, "xmtp": true }
```

Response

```json
{ "agentId": "agent_123", "status": "deploying" }
```

### GET /agents

Response

```json
[ { "name":"my-agent", "state":"running" } ]
```

### GET /agents/:name/status

Response

```json
{ "name":"my-agent", "state":"running", "vps":"vps-12" }
```

### POST /agents/:name/stop

Request: none

Response

```json
{ "success": true }
```

### GET /agents/:name/logs

Query options: `?tail=100`

Response

```json
{ "logs": "..." }
```

### POST /agents/:name/restart

Response

```json
{ "success": true }
```

### GET /skills

Response

```json
[ { "name":"yield-rebalancer", "category":"DeFi" } ]
```

### POST /agents/:name/skills/install

Request

```json
{ "skill": "yield-rebalancer", "ai": "openai" }
```

Response

```json
{ "success": true }
```

### POST /agents/:name/skills/uninstall

Request

```json
{ "skill": "yield-rebalancer" }
```

Response

```json
{ "success": true }
```

### GET /agents/:name/skills

Response

```json
{ "installed": ["yield-rebalancer"] }
```

### POST /agents/:name/xmtp/send

Request

```json
{ "type":"REPORT", "payload": { "msg": "done" } }
```

Response

```json
{ "messageId": "msg_123" }
```

### GET /agents/:name/xmtp/messages

Response

```json
[ { "type":"ALERT", "payload":{...} } ]
```

### GET /x402/balance

Response

```json
{ "balanceUSDC": 12.5 }
```

### POST /x402/fund

Request

```json
{ "agentName":"my-agent", "amountUSDC": 50 }
```

Response

```json
{ "txHash":"0xabc123" }
```

### GET /x402/history

Response

```json
[ { "txHash":"0xabc123", "amount": 10, "time":"2026-02-28T12:00:00Z" } ]
```

### GET /vps

Response

```json
[ { "name":"my-agent", "ip":"1.2.3.4", "status":"running" } ]
```

### GET /vps/:name/stats

Response

```json
{ "cpu": 12.3, "mem": 2048 }
```

### GET /config/:key

Response

```json
{ "key":"x402.maxSpend", "value": 10 }
```

### POST /config/:key

Request

```json
{ "value": 10 }
```

Response

```json
{ "success": true }
```

### GET /config

Response

```json
{ "network":"base", "x402.maxSpend": 10 }
```

## Curl Examples

Deploy an agent

```bash
curl -X POST https://api.xelvyn.xyz/v1/agents/deploy \
  -H "Authorization: Bearer $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name":"my-agent","template":"yield","network":"base","x402":true}'
```

Check x402 balance

```bash
curl -H "Authorization: Bearer $API_KEY" https://api.xelvyn.xyz/v1/x402/balance
```

Send an XMTP message via API

```bash
curl -X POST https://api.xelvyn.xyz/v1/agents/my-agent/xmtp/send \
  -H "Authorization: Bearer $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"type":"ALERT","payload":{"msg":"Threshold exceeded"}}'
```
