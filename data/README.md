# data/

This folder holds inputs and intermediate artifacts for the pipeline. **It is intentionally shipped empty** (except
this README): everything here is either regenerated deterministically or must not be redistributed.

## What gets created here when you run the notebooks

| Path | Created by | Notes |
|------|------------|-------|
| `corpus.json` | nb 01 | carrier code + injected synthetic tokens (regenerated; `seed=42`) |
| `ground_truth.csv` | nb 01 | injected sensitive-token labels (regenerated) |
| `masked_corpus.json` | nb 02 | masked code per tier (regenerated) |
| `id_maps.json` | nb 02 | placeholder → original identifier maps (regenerated) |
| `meta.json` | nb 01 | carrier source + pinned commit (regenerated) |
| `_fineract/` | nb 01 | sparse clone of the upstream carrier, pinned commit — **not redistributed**, fetched at run time |
| `_py_repo/` | nb 09 (P8) | cloned Python carrier for the language replication — fetched at run time |
| `_adv_cache/` | nb 03/09/11 | on-disk cache of LLM adversary responses (makes re-runs deterministic & free) |
| `risk_samples.csv` | (staged) | per-file recovery values from the live run, used by nb 05 |

## Why it is empty in the archive
- **Regenerable:** `corpus.json`, `ground_truth.csv`, `masked_corpus.json`, `id_maps.json`, `meta.json` are produced
  deterministically by notebooks 01–02, so they are not committed.
- **Not redistributable:** `_fineract/` (Apache-2.0 upstream, fetched at a pinned commit) and `_py_repo/` are external
  code, fetched at run time rather than shipped.
- **Machine-local / large:** `_adv_cache/` is a response cache tied to your API key and runs.

## To populate it
Run the notebooks in order (see the top-level `README.md`). Notebook 01 needs network access on first run to fetch the
pinned carrier; subsequent runs reuse the cache. No real or proprietary data is ever placed here — injected tokens are
synthetic and the synthetic carrier (nb 11) is generated.
