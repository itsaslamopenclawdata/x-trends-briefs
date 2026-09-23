# Tool Note — AWS Strands Harness (on Strands Agents SDK)

**Status:** LAUNCH-PHASE, claims vendor-authored · **Source:** [high-signal/2026-09-23-consciousride-aws-strands-harness.md](../high-signal/2026-09-23-consciousride-aws-strands-harness.md)

- **What:** Open-source (Apache 2.0, verify) batteries-included agent harness from AWS — `create_harness()` gives shell, file editing, memory, pre-tuned defaults; model-agnostic (Bedrock/OpenAI/Anthropic/Google/local).
- **Differentiator claim:** ~28% lower token cost vs Claude Code/Codex-class harnesses across six benches at held accuracy (77% on Terminal Bench, Fable 5 vs Claude Code). AWS-authored → replication required.
- **Dependencies:** Python; model endpoint of choice; local via Ollama-style providers (verify in POC).
- **Security:** ships shell access — isolate, scope permissions, no credentials in env.
- **Vendor lock-in:** low (permissive license, model-agnostic) though ergonomics AWS-flavored; AWS staff confirm all defaults overridable.
- **Alternatives:** Claude Code, Codex, OpenHands, LangGraph runtime, smolagents; adjacent routing layer: Fireworks Nexus.
- **Overlap verdict:** NOT a duplicate of current harnesses — adds the local-model + vendor-neutral axis. POC justified (experiment file); migration only on measured win.
