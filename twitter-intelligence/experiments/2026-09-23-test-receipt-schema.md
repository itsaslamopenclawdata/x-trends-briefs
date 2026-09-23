# Experiment — Agent Test-Receipt Schema (6 fields)

**Status:** PROPOSED (2026-09-23) · **Source analysis:** [high-signal/2026-09-23-qapilot-agent-built-mobile-app-testing.md](../high-signal/2026-09-23-qapilot-agent-built-mobile-app-testing.md)

```text
Experiment: Agent test-receipt schema (6 fields)
Hypothesis: A receipt file (intent · device/env state · build · artifacts · failure slice · replay command) lets a fresh agent session reproduce a prior failure without re-deriving context.
Why test it: Converts one-off eval runs into compounding, transferable test assets.
Expected benefit: Cross-session reproducibility + article-worthy IP.
Required tools: existing pytest/eval harness; one ai-agent-learn repo; 1–2h.
Estimated cost: $0.
Success criteria: a fresh Hermes session reproduces a recorded failure using only the receipt.
Failure criteria: receipts add no information beyond CI logs → drop schema.
Rollback: stop generating receipts; delete template.
Output artifact: TEST_RECEIPT.md template + one filled example in the next ai-agent-learn repo.
```

Kill criterion: if the filled receipt on one real repo adds no replay value over existing CI logs, drop immediately.
