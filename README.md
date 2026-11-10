# Forge Agent Hub

Pay-per-call utility APIs for agents and developers. Settlement is USDC on Base via [x402](https://x402.org). No account, no API key.

**Hub:** https://agent-hub.dentreprise.workers.dev  
**API (original 14 tools):** https://x402-gateway.forge-x402.workers.dev  
**API (wave-1 tools):** https://forge-tools.dentreprise.workers.dev  
**MCP (Streamable HTTP):** https://x402-gateway.forge-x402.workers.dev/mcp  
**Contact:** jqfpxwv7@mail.grokbot.com  
**Languages:** English (default), Français, Deutsch, Español, Italiano, Português, Nederlands (`/`, `/fr`, `/de`, `/es`, `/it`, `/pt`, `/nl`).

Wave-1 tools offer a free trial: add `?demo=1` for a labelled sample (HTTP 200, not live data), and the first 3 successful real calls per IP per UTC day are free. After that, unpaid calls still return a valid x402 v2 402. Original gateway tools do not offer that trial; labelled samples for every catalog tool are at `/demo/{slug}.json` (for example https://agent-hub.dentreprise.workers.dev/demo/iban.json).

Call a paid path once without a payment header (after any free trial). The server returns HTTP 402 and a JSON x402 v2 challenge (`accepts[].amount` is atomic USDC, 6 decimals). Retry with `PAYMENT-SIGNATURE` or `X-PAYMENT`, or use [`@x402/fetch`](https://www.npmjs.com/package/@x402/fetch) (official v2; the older package `x402-fetch` is deprecated v1) or the official Python package [`x402`](https://pypi.org/project/x402/). Copy-paste snippets for those clients, the [forge-agent-mcp](https://github.com/forge-agent-hub/forge-agent-mcp) server, and a LangChain tool wrapper are on the [quickstart](https://agent-hub.dentreprise.workers.dev/quickstart/) and on every tool page.

Two paid playbooks ($3 USDC each) are listed in the catalog: [Become an x402 seller on Cloudflare Workers](https://agent-hub.dentreprise.workers.dev/tools/playbook-x402-seller/) and [Build and publish an MCP server to the official registry](https://agent-hub.dentreprise.workers.dev/tools/playbook-mcp-publish/). `?demo=1` returns the table of contents and an excerpt.

## This repository

Machine-readable catalog of the live API, copied from the hub:

| File | What it is |
|------|------------|
| [catalog.json](./catalog.json) | Tools, prices, endpoints, Apify Actors |
| [openapi.json](./openapi.json) | OpenAPI 3.1, 58 paid paths on two hosts, 402 schema, demo trial |
| [llms.txt](./llms.txt) | Agent-oriented index |
| [llms-full.txt](./llms-full.txt) | Full documentation in one file |
| [x402.json](./x402.json) | x402 resource manifest |
| [mcp.json](./mcp.json) | MCP server description |

Live copies: https://agent-hub.dentreprise.workers.dev/catalog.json and `/openapi.json`, `/llms.txt`, `/.well-known/x402`.

## Related repositories

- [forge-x402-examples](https://github.com/forge-agent-hub/forge-x402-examples) — curl, TypeScript and Python clients
- [forge-agent-mcp](https://github.com/forge-agent-hub/forge-agent-mcp) — open-source MCP server (stdio and Streamable HTTP)

## Try it in 1 call

Labelled demo (wave-1, not live data, not charged):

```bash
curl -sS "https://forge-tools.dentreprise.workers.dev/api/gtin-validate?gtin=3017624010701&demo=1"
```

Or see the 402 challenge on the original gateway:

```bash
curl -sS -D - "https://x402-gateway.forge-x402.workers.dev/api/iban?iban=FR7630006000011234567890189"
```

Expect HTTP 402, then pay with an x402 v2 client. See the examples repository and the [quickstart](https://agent-hub.dentreprise.workers.dev/quickstart/).

## Licence

MIT.
