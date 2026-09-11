# File manifest

Generated from the run directory. Sizes are approximate.

| Path | Size | Records |
|---|---|---|
| `data/corpus/corpus.jsonl` | 740 KB | 427 articles |
| `data/corpus/extraction_quality.jsonl` | 3.8 KB | 13 sources |
| `data/corpus/file_map.csv` | 325 B | — |
| `data/corpus/ALL_Annt-26.xlsx` | 126 KB | 331 rows |
| `data/instrument/requirement_units.json` | 822 KB | 264 units |
| `data/instrument/requirement_units_core.json` | 211 KB | pruned set |
| `data/instrument/requirement_units_transposable.json` | 145 KB | 171 units |
| `data/instrument/transposability_screening.json` | 8.2 KB | 93 excluded |
| `data/instrument/_ru_raw.jsonl` | 766 KB | per-article output |
| `data/reference_kb/reference_raw.json` | 102 KB | 2 sources |
| `data/reference_kb/guard_selftest.json` | 122 B | — |
| `data/reference_kb/labeling_functions.jsonl` | 68 KB | weak labels |
| `data/index/index.faiss` | 1.0 MB | — |
| `data/index/index_meta.parquet` | 170 KB | — |
| `data/index/vecs.npy` | 1.0 MB | — |
| `results/records/main.jsonl` | 7.8 MB | 1,584 |
| `results/records/main_transposable.json` | 5.8 MB | 1,026 |
| `results/records/main_records.csv` | 4.7 MB | 1,026 |
| `results/records/stability.jsonl` | 3.9 MB | 594 |
| `results/perturbations/mutations.jsonl` | 564 KB | 148 |
| `results/perturbations/mutation_runs.jsonl` | 981 KB | 145 |
| `results/perturbations/negative_controls.jsonl` | 398 KB | 195 |
| `results/perturbations/metamorphic.jsonl` | 12.6 KB | 66 |
| `results/ablation/ablation.jsonl` | 2.7 MB | 480 |
| `results/ablation/ablation_mutations.jsonl` | 1.8 MB | 290 |
| `results/metrics/metrics.json` | 8.2 KB | — |
| `results/metrics/slot_diagnostic.csv` | 494 KB | 12,686 slots |
| `results/traces/llm_calls.jsonl` | 52 MB | 14,646 calls |
| `figures/` | ~2 MB | 13 figures, PNG + PDF |

**Total** approximately 85 MB. Files above 50 MB require Git LFS; see
`.gitattributes`.
