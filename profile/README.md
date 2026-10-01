<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/wasit-dev/Wasit/main/frontend/public/logo-light.svg" />
  <img src="https://raw.githubusercontent.com/wasit-dev/Wasit/main/frontend/public/logo-dark.svg" alt="Wasit" width="320" />
</picture>

### Protocol-compliance testing for x402 and MPP on Stellar

Wasit runs the real payment flow against a service, then checks the settlement on
Stellar itself: from the token contract's own transfer event, not the service's 200 OK.

[Website](https://usewasit.dev) ·
[Docs](https://usewasit.dev/docs/overview/wasit) ·
[Repository](https://github.com/wasit-dev/wasit) ·
[Check Catalogue](https://github.com/wasit-dev/wasit/blob/main/docs/CHECKS.md) ·
[X](https://x.com/wasithq)

[![@wasit-dev/cli](https://img.shields.io/npm/v/@wasit-dev/cli?label=%40wasit-dev%2Fcli&color=9d6bff)](https://www.npmjs.com/package/@wasit-dev/cli)
[![@wasit-dev/server](https://img.shields.io/npm/v/@wasit-dev/server?label=%40wasit-dev%2Fserver&color=9d6bff)](https://www.npmjs.com/package/@wasit-dev/server)
[![@wasit-dev/core](https://img.shields.io/npm/v/@wasit-dev/core?label=%40wasit-dev%2Fcore&color=9d6bff)](https://www.npmjs.com/package/@wasit-dev/core)
[![CI](https://github.com/wasit-dev/wasit/actions/workflows/ci.yml/badge.svg)](https://github.com/wasit-dev/wasit/actions/workflows/ci.yml)

</div>

<table>
  <tr>
    <td width="50%" valign="top" align="center">
      <img src="https://raw.githubusercontent.com/wasit-dev/Wasit/main/docs/media/x402-0.6.0.gif" width="400" alt="The wasit CLI running the x402 checks: five read-only, then all seven, with the payment's settlement verified on-chain" />
      <br />
      <sub><b>CLI</b> · catalogue, read-only 5/5, then 7/7 with the settlement verified on-chain</sub>
    </td>
    <td width="50%" valign="top" align="center">
      <img src="https://raw.githubusercontent.com/wasit-dev/Wasit/main/docs/media/mcp-0.6.0.gif" width="400" alt="Claude Code calling the same checks over MCP: x402 7/7, then MPP charge and channel" />
      <br />
      <sub><b>MCP</b> · the same checks from Claude Code: x402, then MPP charge and channel</sub>
    </td>
  </tr>
</table>

## Try it, nothing paid

```bash
npx @wasit-dev/cli test --target https://your-service.example/paid --read-only
```

That runs `X402-01` to `X402-05`: no keys, no payment. Drop `--read-only` and add a
testnet key for the checks that settle a real payment.

## One suite, three ways in

| | Package | For |
|---|---|---|
| **CLI** | [`@wasit-dev/cli`](https://www.npmjs.com/package/@wasit-dev/cli) | The `wasit` command, in a terminal or a CI job |
| **MCP** | [`@wasit-dev/server`](https://www.npmjs.com/package/@wasit-dev/server) | The same checks as tools for Claude Code, Claude Desktop and other MCP clients |
| **Core** | [`@wasit-dev/core`](https://www.npmjs.com/package/@wasit-dev/core) | The check suite itself, for your own tooling |

## Thirteen checks

| Protocol | Checks | What they establish |
|---|---|---|
| x402 | `X402-01`–`07` | The 402 challenge is well formed, a valid payment settles on-chain for exactly the advertised terms, and a forged signature is refused |
| MPP charge | `MPP-01` | The charge settles on-chain for the advertised amount, recipient and token |
| MPP channel | `MPP-10`–`14` | The channel matches what was advertised, stale and replayed commitments are refused with 402, and closing settles (opt-in) |

<sub>Testnet only · Apache-2.0 · Each check is traced to a spec clause in the
[Check Catalogue](https://github.com/wasit-dev/wasit/blob/main/docs/CHECKS.md).</sub>
