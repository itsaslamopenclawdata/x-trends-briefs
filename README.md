# X Trends Briefs — AI Learning Radar

Daily synthesized briefs from X (Twitter) across 12 AI topics, generated with the
`x-trends-synthesis` Hermes skill backed by the local `twitter-mcp` server.

## Topics covered

AI agents · LangGraph / multi-agent · RAG · MCP (Model Context Protocol) ·
enterprise AI · AI entrepreneurship · AI Solopreneur using AI Agents ·
Solopreneur using AI Agents · AI Solopreneur · Google ADK ·
AI Coding Workflows · AI Coding Tools

## Structure

- `briefs/YYYY-MM-DD.md` — one file per run: trend summary per topic, key tweets
  with engagement, practical (non-hype) takeaways, practice actions, money angles,
  and a ranked cross-topic "do-next" list.
- `deep-dives/YYYY-MM-DD-<slug>.md` — single-post deep-dive analyses: archived post,
  claim decode, evidence check, signal quality, practical viability, goal scorecard,
  counter-steelman, and a verdict + action plan. `deep-dives/INDEX.md` is the ledger
  (status + retro review dates), `deep-dives/authors.md` tracks author credibility,
  `deep-dives/claims.md` is the recurring-claims register.

## How it works

1. The skill calls `x_trends_brief` on the `twitter-mcp` Hermes MCP server
   (X API v2 `search/recent`, 7-day window, merged into a rolling local archive
   for effective 10+ day coverage from the 2nd run onward).
2. The agent synthesizes the fetched tweets into the brief. Facts and methods are
   stated conservatively — claims from tweets are attributed, not endorsed.
3. The dated brief is committed and pushed here.

## Disclaimer

Briefs summarize what practitioners are discussing on X. Engagement rank ≠ truth.
Verify before acting; the brief flags unverified claims where spotted.
