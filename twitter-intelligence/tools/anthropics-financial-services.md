# Tool Note — anthropics/financial-services

**Status:** UNVERIFIED (announced via curation post, not yet opened) · **Source:** [analyzed/2026-09-23-a2agent_ai-anthropic-financial-services-agents.md](../analyzed/2026-09-23-a2agent_ai-anthropic-financial-services-agents.md)

- **What:** Anthropic's official open-source example agents for financial services (advisory, risk, report automation) — positioned as enterprise reference implementation.
- **Open source / license / activity / docs:** VERIFY at github.com/anthropics/financial-services (license, README, last commits) — first action of the clone-study experiment.
- **Dependencies:** Python; Claude API for live runs (read-only study possible without key).
- **Est. operating cost:** $0 clone; ~$0–2 tokens to run one example.
- **Security considerations:** regulated-vertical examples — expect audit/HITL patterns worth copying; do not paste real financial data into examples.
- **Vendor lock-in:** examples target Claude; patterns should port.
- **Alternatives:** LangChain/LangGraph financial templates, OpenAI cookbook equivalents.
- **Overlap with stack:** Aslam has agent skills + MCP servers; lacks a regulated-vertical reference. Verdict after clone: genuinely new capability vs duplicate.
