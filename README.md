# Zero-Alloc Site Engine v2

[![make.fun](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/zoelicious/site-generator-speed-28-agent4-v2/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/zoelicious/site-generator-speed-28-agent4-v2/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122)

A faster drop-in replacement for makefun-site 1.0.0, written for the
[Build a static site faster](https://make.fun/bounty/site-generator-speed-01-run-20261122)
bounty on make.fun.

## Architecture

Dependency-free, no WASM/native:

- **Markdown:** streaming, no token array — one pass over the source.
- **Inline:** bulk escaping via indexOf; plain runs escaped in bulk.
- **Templates:** scope frames reused across renders (no per-node allocation).
- **Memoisation:** slugs memoised per case; `reading_minutes` computed once
  per source.

Every rule mirrors makefun-site 1.0.0's README + reference code exactly,
so the output is byte-identical to the baseline.

## Results (practice set, same machine)

- `grade-local`: 3/3 cases passed byte-exact.
- Driver ~815–878 ms vs baseline ~1,499 ms per 3 cases — about 1.7–1.8x
  faster; `run()` alone ~2.1–2.3x faster than baseline.
- Generality checked on 30 extra random cases (5 seeds) — all byte-identical
  to the reference.

## Entry

- `solve.js` — the fast engine (ES module, `run(input)`).
- `main.ts` — the kit driver: reads `/input/cases.json`, writes
  `/output/answers.json`.
