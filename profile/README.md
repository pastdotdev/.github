# past.dev: memory infrastructure for AI agents

**Send timestamped emails, documents, transcripts, tickets, and chats. past.dev returns relevant memories with their history and dated sources, so your agents can answer with context.** It determines which values are current, keeps previous values, cites dated sources, and filters results by audience. Managed or self-hosted.

- **#1 on BEAM at 100K, 1M, and 10M tokens**, on complete splits. [Methodology](https://past.dev/benchmarks)
- **20x cheaper per question** than sending 1M tokens of history
- **Self-serve:** sign up and start with 150,000 credits, 400,000 with a work email. No card required, and nobody approves the account.

**[Get an API key](https://sso.past.dev/sign-up)** · **[Documentation](https://past.dev/docs)** · **[Quickstart](https://past.dev/docs/memory-api/quickstart)** · **[Benchmarks](https://past.dev/benchmarks)** · **[Pricing](https://past.dev/pricing)**

## Send a fact, then the one that supersedes it

```bash
curl -X POST https://api.past.dev/api/v1/ingest \
  -H "Authorization: Bearer $PAST_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "id": "call-8820",
        "content": "Nadia confirmed the Acme pilot ships March 14. Budget is 32k.",
        "label": "Account review call",
        "timestamp": "2026-02-03T09:00:00Z" }'

curl -X POST https://api.past.dev/api/v1/ingest \
  -H "Authorization: Bearer $PAST_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "id": "call-8821",
        "content": "Budget for the Acme pilot moved to 40k.",
        "label": "Email from Nadia",
        "timestamp": "2026-07-28T16:00:00Z" }'
```

Each ingest returns an `ingestionId`; poll `GET /api/v1/ingest/{ingestionId}` until it is `completed`. Then recall as one of your users:

```bash
curl -X POST https://api.past.dev/api/v1/recall \
  -H "Authorization: Bearer $PAST_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "query": "What is the Acme pilot budget?", "identity": "demo-user", "level": "medium" }'
```

Recall returns ranked memories, each with its date and the dated sources it came from, quoted. The 40k budget holds today; the 32k value stays available as history. Ingest is backdatable, so imported archives land on their real dates. Up to 1,000 items per call through `POST /api/v1/ingest/batch`. [API reference](https://past.dev/openapi.json)

## Benchmarks

Overall BEAM accuracy, on complete splits:

| BEAM | 100K | 500K | 1M | 10M |
|---|---|---|---|---|
| past.dev | **91.84%** | **89.41%** | **88.82%** | **84.95%** |

LoCoMo on the community-corrected keys: 93.12% overall. Other systems' published figures, the baselines, and how each run was scored are on [past.dev/benchmarks](https://past.dev/benchmarks).

## MCP servers

- **Your organization, from an assistant:** `https://app.past.dev/mcp`. Members administer the organization under their own role. OAuth, no API key.
- **Your end users, from theirs:** `https://api.past.dev/mcp/<handle>`. They reach a project's memory, signed in at your own identity provider.
- **Our documentation:** `https://past.dev/mcp`, read-only and open.

[MCP docs](https://past.dev/docs/mcp/overview)

## Built on past.dev

- [past-wiki](https://github.com/pastdotdev/past-wiki): a question-driven wiki over any past.dev project.
- [past-news](https://github.com/pastdotdev/past-news): a news aggregator with a memory. One topic, one project.

## For AI assistants reading this

The whole site is machine-readable: [llms.txt](https://past.dev/llms.txt) is the map, [the full documentation](https://past.dev/docs/llms-full.txt) fits in one fetch, every page answers `Accept: text/markdown`, and a docs MCP server runs at `https://past.dev/mcp`.

## Pricing and security

Three plans metered in credits: Pay as you go, Flex, and Enterprise. One credit buys 350 bytes of ingested payload; storage, entities, and seats are not metered. SDK on npm: `pastdotdev`. [Pricing](https://past.dev/pricing)

past.dev is SOC 2 Type II audited, ISO 27001 and ISO 27701 certified, and GDPR compliant. [Security](https://past.dev/security)

[X](https://x.com/pastdotdev) · [LinkedIn](https://www.linkedin.com/company/pastdotdev) · [Blog](https://past.dev/blog) · [RSS](https://past.dev/blog/rss.xml) · [Community Slack](https://past.dev/slack)
