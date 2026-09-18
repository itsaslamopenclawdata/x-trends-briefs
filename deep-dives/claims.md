# Claims Register

Distinct factual claims extracted from deep-dives. One row per claim — update in place
(new sources, status changes), never duplicate. `status`: VERIFIED · UNVERIFIED ·
DEBUNKED · CORROBORATED (≥3 independent sources).

| claim | first_seen | sources | status | how_to_verify |
|-------|-----------|---------|--------|---------------|
| ChatGPT "Sites" (Astra) builds/hosts/publishes websites from prompts on client domains; $20/mo Plus; unavailable EEA/CH/UK at launch | 2026-09-18 | @0xchromium/2100225265162936516 | PARTIALLY VERIFIED (release tweet confirmed; feature/pricing/regions UNVERIFIED) | OpenAI model card + Sites docs; ToS on client work per seat tier |
| Astra scores 57.9% on Terminal-Bench 4.0 vs 37.3% previous | 2026-09-18 | @0xchromium/2100225265162936516 | UNVERIFIED | OpenAI model card / Terminal-Bench leaderboard |
| SMB website maintenance plans ($150–900/mo) reach $10k MRR at 15–20 clients | 2026-09-18 | @0xchromium/2100225265162936516 | UNVERIFIED (arithmetic checks; zero execution evidence) | The bounded spike itself — 5-preview outreach test |
| A dual-model split (exec brain + parallel engine, e.g. GPT-6 Astra + Kimi K3) beats single-model for personal AI-OS workflows | 2026-09-18 | @de1lymoon/2098714638552559806 | UNVERIFIED | Build dual-vs-single spike with eval harness (accuracy/cost/latency); article body itself also unread (auth-walled) |
