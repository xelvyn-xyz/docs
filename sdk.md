# TypeScript SDK Reference

Install

```bash
npm install @xelvyn/sdk
```

Import

```ts
import { XelvynClient, XelvynError } from '@xelvyn/sdk'
```

## XelvynClient

Constructor

```ts
new XelvynClient({
  apiKey: string,           // required
  network?: string,        // default: 'base'
  baseUrl?: string,        // optional custom API URL
  x402?: {                 // optional x402 config
    enabled?: boolean
  }
})
```

## Namespaces

All methods return Promises. Errors are instances of `XelvynError` with `statusCode` and `responseBody`.

### agents

Methods

- `deploy(name: string, options?: { network?: string, x402?: boolean, xmtp?: boolean }): Promise<{ agentId: string }>`
- `status(name: string): Promise<{ name:string, state:string, vps:string }>`
- `list(): Promise<Array<{ name:string, state:string }>>`
- `stop(name: string): Promise<{ success: boolean }>`
- `logs(name: string, opts?: { tail?: number, level?: string }): Promise<string>`
- `restart(name: string): Promise<{ success: boolean }>`

Example

```ts
const client = new XelvynClient({ apiKey: process.env.XELVYN_API_KEY })
await client.agents.deploy('my-agent', { network: 'base', x402: true, xmtp: true })
```

### skills

Methods

- `list(): Promise<Array<{ name:string, category:string }>>`
- `install(agentName: string, skill: string, opts?: { ai?: 'openai'|'claude' }): Promise<{ success: boolean }>`
- `uninstall(agentName: string, skill: string): Promise<{ success: boolean }>`
- `installed(agentName: string): Promise<Array<string>>`

Example

```ts
await client.skills.install('my-agent', 'yield-rebalancer', { ai: 'openai' })
```

### xmtp

Methods

- `send(agentName: string, message: { type: string, payload: any }): Promise<{ messageId: string }>`
- `messages(agentName: string, opts?: { since?: string }): Promise<Array<any>>`

Example

```ts
await client.xmtp.send('my-agent', { type: 'DEPLOY', payload: { status: 'ok' } })
const msgs = await client.xmtp.messages('my-agent')
```

### x402

Methods

- `balance(agentName?: string): Promise<{ balanceUSDC: number }>`
- `fund(agentName: string, amountUSDC: number): Promise<{ txHash: string }>`
- `history(agentName?: string): Promise<Array<any>>`

Example

```ts
const bal = await client.x402.balance('my-agent')
await client.x402.fund('my-agent', 50)
```

### vps

Methods

- `list(): Promise<Array<{ name:string, ip:string, status:string }>>`
- `stats(name: string): Promise<{ cpu:number, mem:number, disk:number }>`

### config

Methods

- `get(key: string): Promise<any>`
- `set(key: string, value: any): Promise<void>`
- `list(): Promise<Record<string, any>>`

### Errors

Class `XelvynError` extends `Error` and includes:

- `statusCode?: number`
- `responseBody?: any`

Example error handling

```ts
try {
  await client.agents.deploy('my-agent')
} catch (e) {
  if (e instanceof XelvynError) {
    console.error('API error', e.statusCode, e.responseBody)
  }
}
```
