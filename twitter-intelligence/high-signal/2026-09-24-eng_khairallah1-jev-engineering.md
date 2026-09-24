# Jev Engineering build guide (Khairallah) — xintel

- **Source:** https://x.com/eng_khairallah1/status/2102767762829447540 | **Author:** @eng_khairallah1 (Khairallah AL-Awady) | **Date:** 2026-09-23 (posted) / 2026-09-24 (xintel)
- **Post ID:** 2102767762829447540 | **Engagement:** ❤71 🔁19 💬25 🔖96 👁31571 | **Mode:** api-fetch + attached article (full; middle from local cache)
- **Type:** Agentic AI · Architecture · Cost Optimization · Tutorial · Dev Tool
- **Corroboration:** Theme CORROBORATED (radar `jev` 2, `typesafe` 1; DailyLogsHermes already ships `tools/jev/`). This *article* is LONE (new today). Opposite of @0xMovez 200×/400× PDF and @Sprytixl leak-spam: this one publishes failure modes and benchmark caveats.
- **Body:** full (~20k chars).
- **Dedup:** tweet_id not in INDEX.

## Original Post

> Jev is the missing brain in every AI agent. It decides what happens next in milliseconds, at almost zero cost. Set it up right and you cut most of your agent bill without touching quality.
>
> **X Article:** "Jev Engineering: How to Actually Build Your First AI Agent Brain (from scratch)"
>
> @eng_khairallah1 · following 1986 · posted 2026-09-23T14:31:16Z

**Thesis:** Frontier LLMs are rented System 2 to return the word “billing.” Jev = System 1: state + typed questions → parallel typed answers + probabilities. No generation.

**Vendor claims (UNVERIFIED except as TypeSafe marketing):** TypeSafe stealth 2026-09-15, $40M DCVC, Diogo Almeida / RLHF-InstructGPT. 70–500 ms; $0.042 / M input; **output tokens free**. 64k combined state+questions; 32k state+longest question.

**Three-bucket split (the durable part):**
1. **Creates text → LLM** (brief, email, code, explanation). Jev cannot generate.
2. **Pick / score / yes-no → Jev**
3. **Exact rule → code** (caps, counts, dates). Biggest savings = skip *both* models.

**Three primitives:** `Choice` (≤255 options; always include `other`; returns choice, probabilities, confidence). `Score` (2–10 ordered levels; score can land *between* levels). `Noul` (P(yes) in [0,1]; no separate confidence). **Jev never sees your Python field name** — instructions + criteria only.

**Patterns:** pin `jev-1.13.0` not `jev-latest`. Per-action confidence (read-only low bar; money/send high bar + human). Ask all questions in one round trip (cookbook: 13-q batch ~12× cheaper / 10× faster vs sequential — **vendor cookbook**). Cascade: Jev decides *which* requests deserve an LLM. Code owns irreversible: prepare, then approve.

**Cited third-party (UNVERIFIED):** @nutlope 1,018 papers: DeepSeek summarize $3.99 vs Jev classify $0.08 / 256 ms median. Browser Use Google Flights **found** (did not book) ZRH–LHR 7.1 s / $0.0039. @altryne Claude plugin 1M→86k tokens in ~1 s. @tamarajtran compaction via scoring tool calls.

**Failure modes (TypeSafe jaggedness page, restated):** reads literally (negations); not a calculator; dates are text; context rot; no world knowledge beyond state; **state is not hostile** (prompt-injection on user text in state). Rate limits claimed 250k tok/s, 1,200 rpm. Log model version + probabilities + confidence.

**Honest scorecard:** TypeSafe four-workflow eval **~67.8%** — mid-tier agreement, not accuracy. Labels = average of two frontier models. Self-run. “Cannot hallucinate” = cannot leave schema; **can pick the wrong valid value**. Price may be subsidized.

**Replies:** 256 ms nice; Japanese summary; “skeptical how much it saves when LLMs already generate huge context around coding decisions.”

## Executive Summary

### What happened?
A same-day build guide for TypeSafe Jev that is unusually adult: primitives, cascade, jaggedness, and “67.8% is agreement, not accuracy.” 32k views, not a million-view wealth article.

### Why is it important?
DailyLogsHermes **already has** `tools/jev/` (router + quality gate, 20 offline tests, live tests, fallback). This post is a **checklist against the live layer**, not a reason to install Jev again. Phase 2–4 in `docs/jev-routing-policy.md` (model/tool/risk routers) are still OFF — this article is the spec those phases should steal from.

### What is actually new? (vs our Jev docs)
We have: choice routing, PASS/REVIEW/RETRY/ESCALATE gate, **one** 0.60 confidence threshold, deterministic checks first, cache routing only.  
This article adds: **Score + Noul**, **per-action** thresholds, **batch questions**, pin version, jaggedness (don’t count/date in Jev), state-not-hostile, “exact rules never touch a model.” Those are the gaps.

### Why might this matter to me?
#1/#2/#7: the decision layer you already paid to build. Highest-leverage Jev post this week. Ignore $40M / Almeida biography.

## Key Takeaways

| # | Takeaway | Importance | Application | Actionability |
|---|----------|-----------|-------------|---------------|
| 1 | LLM writes; Jev decides; **code executes and owns irreversible** | High | Jev policy | Already mostly true; tighten “prepare then approve” |
| 2 | Biggest savings = skip models via exact rules, not cheaper Jev | High | Caps, counts, tests | LEARN |
| 3 | Per-action confidence, not one 0.60 | High | `jev-routing-policy.md` | EXPERIMENT |
| 4 | Batch questions (parallel, ~free latency) | Med | SDK calls | EXPERIMENT if live traffic exists |
| 5 | Pin model version; log version+probs | High | config.py | EXPERIMENT |
| 6 | Jev is not a calculator / not a date engine / reads literally | High | Tests | Add negative tests |
| 7 | 67.8% is **agreement with two LLMs**, self-run | High | Filter | Don’t cite as accuracy |
| 8 | Reply skepticism: coding agents generate context around decisions — Jev may save less there | Med | Scope | Measure on *your* gate traffic |

## Claims & Evidence

| Claim | Type | Confidence | Why | Verification needed |
|-------|------|-----------|-----|---------------------|
| 70–500 ms; $0.042/M in; output free | BENCHMARK | LOW–MEDIUM | Vendor list price | TypeSafe pricing page + own `test_jev_live` bills |
| 67.8% on 4 workflows | BENCHMARK | LOW as accuracy | Author flags consensus-label + self-run | Own labeled traffic |
| 12× cheaper / 10× faster batched vs sequential | BENCHMARK | LOW | “TypeSafe cookbook” | One live batch vs loop if key present |
| 1,018 papers $0.08 / 256 ms | ANECDOTE | LOW | @nutlope tweet in article | Don’t treat as yours |
| Flight demo 7.1 s / $0.0039 | ANECDOTE | LOW | Found, not booked | — |
| Field names are invisible to Jev | CLAIM | MEDIUM | Matches typed-API design | SDK docs / one live probe |
| State not treated as hostile | CLAIM | MEDIUM | Honest; matches injection class | Test if user text enters gate state |

## Signal Assessment

**HIGH** — first Jev write-up this week that includes jaggedness + benchmark epistemology. Engagement modest (good). Author not a $100k leak mill.

**Red-team:** LEARN only — you already shipped Jev; this is a blog; waitlist/API spend is YELLOW; 67.8% is circular. Disagrees with EXPERIMENT by one tier. **Reconcile:** EXPERIMENT = **2h gap list vs `tools/jev/`**, no new product, no new key. If the list is “already have it” → LEARN and close.

## Relevance

#1 agent architecture, #2 production/cost, #3 eval (calibrated confidence, don’t trust 0.60 globally), #7 workforce. Direct hit.

## Opportunity

| Lane | Finding |
|------|---------|
| Technical | Per-action thresholds; Noul/Score; jaggedness tests; pin version |
| Product | None |
| Learning | Three-bucket split as a written checklist |
| Business | None |
| Automation | Batch questions if live Jev is on |
| Integration | Diff vs `docs/jev-routing-policy.md` Phase 2–4 |

## Tool Assessment

**Jev / typesafe-sdk** — already in repo. **Duplicate if re-installed.** Early access waitlisted. Price may be subsidized. Do not add a second client.

## Implementation Possibilities

**EXPERIMENT** (gap list). Not BUILD PRODUCT. Not new INTEGRATE.

**Goal:** 15-line diff: article patterns vs `tools/jev/` + routing policy. Tick: global vs per-action threshold; Score/Noul unused?; version pin; batching; calculator/date negative tests.

**Steps:** read policy + config.py → tick list → optional one live call **only if** `TYPESAFE_API_KEY` already present → stop.

**Kill:** creating a new TypeSafe account, or >2h, or using Jev to fire a send.

## Hermes Recommended Actions

| Action | Priority | Safety gate |
|--------|----------|-------------|
| EXPERIMENT: 2h Jev gap list vs this article (per-action conf, pin version, jaggedness tests) | THIS WEEK | GREEN |
| Do **not** open a new TypeSafe waitlist / new key unless gap requires a primitive you don’t have | IGNORE | YELLOW avoided |
| Do **not** treat 67.8% / $0.042 / 200× viral PDF as facts | — | GREEN |
| Queue **ahead of** chalkline-vs-Jev (same layer; this is closer to live code) | DO NOW | GREEN |
| standing-ops-nine still first if send-gate hole exists | THIS WEEK | GREEN |

## Experiment

```
Experiment: jev-article-gap-list
Hypothesis: live Jev is Choice+one-threshold only; Score/Noul, per-action bars, version pin, and “not a calculator” tests are missing.
Why: this is the first honest Jev build guide; we already have the SDK.
Expected benefit: 1–3 policy/test patches, $0.
Required tools: D:\DailyLogsHermes\tools\jev + docs (no new key).
Estimated effort: 2 hours
Estimated cost: $0 (live calls only if key already there)
Success criteria: gap list written; at most one small patch (pin version OR a negative test).
Failure criteria: new vendor account; wiring Jev to send/spend; >2h.
Rollback: revert the one patch.
Output: note in docs/ or Weekly Experiments Lab.
```

## ROI Assessment

Value: High (if gaps) · Effort: Low · Cost: Low · Risk: Low · Learning: High · Business: Low · Automation: Med  
Priority: this week, after send-gate check, before chalkline clone.

## Business Potential

None from the article. TypeSafe’s, not yours.

## Verification Needed

- Own live bills vs $0.042/M.
- 67.8%: never cite as accuracy.
- Field-name invisibility: one probe if key exists.

## Final Decision

**EXPERIMENT** — 2h gap list against **existing** `tools/jev/`. Steal the three-bucket split, per-action confidence, pin version, jaggedness. Do not re-onboard TypeSafe. Do not confuse this with 200× viral Jev PDFs.

Red-team: LEARN. Reconcile: EXPERIMENT with 2h / no-new-key kill.

## Tags

topics: [jev, system-one, confidence-gating, cost]
technologies: [typesafe-sdk, hermes]
opportunity: [jev-gap-list]
action: [experiment]
priority: [this-week-2h]
