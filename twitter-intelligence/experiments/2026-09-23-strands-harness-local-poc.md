# Experiment — Strands Harness Local-Model POC vs Current Harness

**Status:** PROPOSED (2026-09-23) · **Source analysis:** [high-signal/2026-09-23-consciousride-aws-strands-harness.md](../high-signal/2026-09-23-consciousride-aws-strands-harness.md)

```text
Experiment: Strands Harness local-model POC vs current harness
Hypothesis: Strands Harness can drive a local (Ollama) model through one real Mastery-OS-style repo task with pass-rate within 10% of the cloud-harness baseline, at lower $/task.
Why test it: Valid/falsify the vendor cost claims with own data, and open the local-agent path.
Expected benefit: Evidence-based harness decision + reusable comparison methodology (article-worthy).
Required tools: Python 3.11, Ollama (installed), Strands SDK (pip), one ai-agent-learn-style repo with tests, 3–4h.
Estimated cost: ~$0 (local model) + ~$1–3 for the cloud comparison run.
Success criteria: task completes green; measured comparison table produced; ≥1 concrete use-case where local+Strands beats current setup.
Failure criteria: install friction >1h, local-model support not real, or pass-rate >10% below baseline with no compensating advantage → ARCHIVE with note.
Rollback: uninstall package, delete folder; nothing else touched.
Output artifact: TEST_RECEIPT.md (receipt-schema experiment) + trends/strands-harness-poc-results.md
```

Kill criterion note: failure = archive within 24h; do not keep tweaking to make it pass.
