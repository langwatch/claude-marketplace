# LangWatch Claude Code marketplace

A [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) for the LangWatch org. One plugin today: **`langwatch-experts`**.

## Install

```
/plugin marketplace add langwatch/claude-marketplace
/plugin install langwatch-experts@langwatch
```

## What you get

Two delegate-to expert agents, backed by the LangWatch MCP server:

- **`scenario-expert`** — writing, debugging, and reasoning about [Scenario](https://github.com/langwatch/scenario) agent tests (`@langwatch/scenario`): turn-plans/scripts, the judge, simulation runs, and "what can the judge see?" / "why does this message sequence look wrong?" questions.
- **`langwatch-expert`** — the LangWatch observability/evaluation platform: instrumentation, tracing, the trace schema, analytics, and reading what actually happened in a run.

The agents prefer live docs (and, with a key, live traces) over stale priors. **Documentation tools work with NO API key — install is zero-config.** Set the optional `LangWatch API key` at enable time to unlock live traces and observability (`search_traces`, `get_trace`, `get_analytics`, and the `platform_*` tools).

Found a gap in an expert's knowledge? [Open an issue](https://github.com/langwatch/claude-marketplace/issues) — contributions are welcome but never required.

## Automation / CI

The interactive install prompt is the normal way to set your key — paste it once and it's stored; change it any time by re-running the plugin config. The MCP server reads it from there on every launch.

In a headless/scripted run (`claude --plugin-dir ... -p ...`) there is no prompt, so pass the key directly with `--mcp-config` instead:

```json
{
  "mcpServers": {
    "langwatch": {
      "command": "npx",
      "args": ["-y", "@langwatch/mcp-server"],
      "env": { "LANGWATCH_API_KEY": "$LANGWATCH_API_KEY" }
    }
  }
}
```

Docs tools (`fetch_scenario_docs`, `fetch_langwatch_docs`) need no key in either mode.

## Related tools

- **[`@langwatch/mcp-server`](https://www.npmjs.com/package/@langwatch/mcp-server)** — the LangWatch MCP server these agents call for docs, traces, and platform access.
- **[`langwatch/better-agents`](https://github.com/langwatch/better-agents)** — a separate toolkit for *building* agents.
- **[`langwatch/skills`](https://github.com/langwatch/skills)** — LangWatch's skills-CLI capabilities (a separate distribution channel).
