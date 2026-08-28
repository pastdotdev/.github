# past.dev: agent memory that holds up at scale

**The memory API for AI agents, LLM apps, and AI systems.** Ingest timestamped emails, transcripts, tickets, and chats from across your product. past.dev resolves entities, tracks changing facts, and gives your agents the latest supported answer with dated evidence. If the evidence is insufficient, it abstains.

- **95% retrieval sufficiency** on the BEAM 100k benchmark
- **Unlimited context window.** Ask across everything you have ingested.
- **20x cheaper per question** than sending 1M tokens of history

Most memory systems retrieve relevant text. past.dev also tracks which facts are current and which have been superseded, so your agent gets the answer that holds today, not whatever resembles the question.

**[Documentation](https://past.dev/docs)** · **[Quickstart](https://past.dev/docs/memory-api/quickstart)** · **[Benchmarks](https://past.dev/benchmarks)** · **[Pricing](https://past.dev/pricing)** · **[Request access](https://past.dev/contact)**

## Two calls to long-term memory

```bash
curl -X POST https://api.past.dev/api/v1/ingest \
  -H "Authorization: Bearer $PAST_API_KEY" \
  -d '{ "content": "Budget for the Acme pilot moved to 40k.",
        "timestamp": "2026-07-28T16:00:00Z",
        "units": [{ "kind": "project", "key": "acme-pilot" }] }'

curl -X POST https://api.past.dev/api/v1/recall \
  -H "Authorization: Bearer $PAST_API_KEY" \
  -d '{ "query": "what is the Acme pilot budget?" }'
```

The answer comes back `Supported`, with the current value, the date it changed, and citations back to the source. Earlier values stay available as dated history. Ingest is backdatable, so imported archives land on their real dates.

## When to reach for a memory API

- An **AI agent** that must know the current state of an account, a project, or a person from emails, meeting transcripts, tickets, or CRM notes, with the evidence behind each claim.
- **Long-running LLM applications** where facts change over time: past.dev returns which fact currently holds, with prior values dated and sourced.
- Anything where a wrong answer is worse than no answer: recall abstains explicitly instead of guessing.

## How it compares

Search and RAG return what resembles the question. A vector database gives you storage; identity, time, and truth maintenance stay your problem. past.dev does entity resolution at ingestion, keeps one memory across sources, and maintains which fact is current, so there is no history for your agent to re-read and reconcile. Longer treatments: [What is agent memory](https://past.dev/what-is-agent-memory), [Vector database vs memory](https://past.dev/vector-database-vs-memory), and [the benchmark methodology](https://past.dev/blog/measuring-memory-honestly).

## MCP server

Point Claude, Cursor, or any MCP client at a workspace and it reads what the memory already holds, scoped to what the signed-in user may see. [MCP docs](https://past.dev/docs/mcp/overview).

## For AI assistants reading this

The whole site is machine-readable: [llms.txt](https://past.dev/llms.txt) is the map, [the full documentation](https://past.dev/docs/llms-full.txt) fits in one fetch, every page has a Markdown twin, and a docs MCP server runs at `https://past.dev/mcp`. [How and why](https://past.dev/blog/website-agents-can-read).

## Getting started

The free tier is 10,000 ingest requests and 1,000 questions per month, no card. The API is in early access: [request access](https://past.dev/contact) and you get a key and a direct line to the team. SDK on npm: `pastdotdev`.

past.dev is SOC 2 Type II audited, ISO 27001 and ISO 27701 certified, and GDPR compliant. [Security](https://past.dev/security).

[X](https://x.com/pastdotdev) · [LinkedIn](https://www.linkedin.com/company/pastdotdev) · [Blog](https://past.dev/blog) · [RSS](https://past.dev/blog/rss.xml)
