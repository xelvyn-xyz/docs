# CLI Reference

The `@xelvyn/cli` is the primary command-line interface for deploying and managing agents.

Usage: `xelvyn <command> [options]`

Commands

1) `login`

Syntax

```bash
xelvyn login
```

Flags: none

Example output:

```
Opening browser for authentication... Success. Logged in as operator@example.com
```

2) `init`

Syntax

```bash
xelvyn init <name> --template <template> --network <network> [--x402]
```

Flags

- `--template` (required): `yield|monitor|router|custom`
- `--network` (optional): default `base`
- `--x402` (optional): initialize x402 channels

Example

```bash
xelvyn init my-agent --template yield --network base --x402
```

Example output:

```
Scaffolded agent 'my-agent' using template 'yield'. .env created. x402 set up pending funding.
```

3) `deploy`

Syntax

```bash
xelvyn deploy <name> --network <network> [--x402] [--xmtp] [--dry-run]
```

Flags

- `--network`: network to deploy to (default: `base`)
- `--x402`: enable x402 payments
- `--xmtp`: enable XMTP messaging
- `--dry-run`: show actions without performing them

Example

```bash
xelvyn deploy my-agent --network base --x402 --xmtp
```

Example output:

```
Provisioning VPS... Done
Installing runtime... Done
Deploying agent... Done
Agent 'my-agent' deployed and running. Monitor with `xelvyn status my-agent --live`.
```

4) `status`

Syntax

```bash
xelvyn status <name> [--live] [--json]
```

Flags

- `--live`: stream live status
- `--json`: print machine-readable JSON

Example

```bash
xelvyn status my-agent --live
```

5) `logs`

Syntax

```bash
xelvyn logs <name> [--tail <n>] [--follow] [--level <info|warn|error|debug>]
```

Flags

- `--tail`: show last N lines
- `--follow`: follow logs (like `tail -f`)
- `--level`: filter by log level

6) `stop`

Syntax

```bash
xelvyn stop <name> [--force]
```

- `--force`: forcibly stop the VPS and processes

7) `config`

Subcommands: `list`, `get <key>`, `set <key> <value>`

Example

```bash
xelvyn config set x402.maxSpend 10
xelvyn config get x402.maxSpend
xelvyn config list
```

8) `whoami`

Syntax

```bash
xelvyn whoami
```

Output: operator identity

9) `skill`

Subcommands: `install <name> [--ai openai|claude]`, `list`

Example

```bash
xelvyn skill install yield-rebalancer --ai openai
xelvyn skill list
```

10) `x402`

Subcommands: `balance`, `fund <amount>`, `history`

Examples

```bash
xelvyn x402 balance
xelvyn x402 fund 50
xelvyn x402 history
```

11) `vps`

Subcommands: `list`, `stats <name>`, `ssh <name>`

Examples

```bash
xelvyn vps list
xelvyn vps stats my-agent
xelvyn vps ssh my-agent
```

Common flags and behavior

- Use `--json` with commands to receive machine-readable output.
- Use `--dry-run` where available to preview destructive or billing actions.
