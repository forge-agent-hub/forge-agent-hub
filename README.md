# Forge Agent Hub

Pay-per-call utility APIs for agents and developers. Settlement is USDC on Base via [x402](https://x402.org). No account, no API key.

**Hub:** https://agent-hub.dentreprise.workers.dev  
**API (original 14 tools):** https://x402-gateway.forge-x402.workers.dev  
**API (wave-1 tools):** https://forge-tools.dentreprise.workers.dev  
**MCP (Streamable HTTP):** https://x402-gateway.forge-x402.workers.dev/mcp  
**Contact:** jqfpxwv7@mail.grokbot.com

Call a paid path once without a payment header. The gateway returns HTTP 402 and a JSON x402 v2 challenge (`accepts[].amount` is atomic USDC, 6 decimals). Retry with `PAYMENT-SIGNATURE` or `X-PAYMENT`, or use [`@x402/fetch`](https://www.npmjs.com/package/@x402/fetch).

## This repository

Machine-readable catalog of the live API, copied from the hub:

| File | What it is |
|------|------------|
| [catalog.json](./catalog.json) | Tools, prices, endpoints, Apify Actors |
| [openapi.json](./openapi.json) | OpenAPI 3.1, 43 paid paths on two hosts, 402 schema |
| [llms.txt](./llms.txt) | Agent-oriented index |
| [llms-full.txt](./llms-full.txt) | Full documentation in one file |
| [x402.json](./x402.json) | x402 resource manifest |
| [mcp.json](./mcp.json) | MCP server description |

Live copies: https://agent-hub.dentreprise.workers.dev/catalog.json and `/openapi.json`, `/llms.txt`, `/.well-known/x402`.

## Related repositories

- [forge-x402-examples](https://github.com/forge-agent-hub/forge-x402-examples) — curl, TypeScript and Python clients
- [forge-agent-mcp](https://github.com/forge-agent-hub/forge-agent-mcp) — open-source MCP server (stdio and Streamable HTTP)

## Try it in 1 call

```bash
curl -sS -D - "https://x402-gateway.forge-x402.workers.dev/api/iban?iban=FR7630006000011234567890189"
```

Expect HTTP 402, then pay with an x402 v2 client. See the examples repository.

## Licence

MIT.
