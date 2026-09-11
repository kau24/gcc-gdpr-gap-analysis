# Multi-Agent Reasoning for Legal Gap Analysis

Provision-level comparison of six GCC personal data protection statutes against the
GDPR, performed by a metacognitively regulated multi-agent system and evaluated
without expert annotation.

This repository contains the code, corpus, instrument, complete execution records and
figures for the paper. Every reported figure can be recomputed from the artefacts here.

## Researchers: 

## What the system does

The GDPR is decomposed into atomic **requirement units**, each represented as an
eight-slot deontic frame: addressee, modality, action, scope, condition, exception,
temporal element, consequence. For each unit and each jurisdiction the system
retrieves candidate provisions, adjudicates the comparison slot by slot with a
verbatim span and citation per slot, and derives an aggregate label by deterministic
rule.

| Label | Meaning |
|-------|---------|
| C1 | Functional equivalence |
| C2 | Partial coverage |
| C3 | Modality divergence |
| C4 | Scope divergence |
| C5 | Absent |

**Architecture.** Bilingual retrieval (FAISS over multilingual sentence embeddings),
slot-wise adjudication (`gpt-5`), adversarial verification on a second model family
(`Llama-3.3-70B-Instruct-Turbo`), and a metacognitive orchestrator monitoring
evidence sufficiency, matching strategy, reasoning completeness and self-consistency.
Control flow is a deterministic state machine; the aggregate label is computed by rule
rather than generated.

![Architecture](figures/D1_architecture.png)

---

## Headline results

Assessment matrix: **171 transposable requirement units x 6 jurisdictions = 1,026
records**, from 14,646 model calls.

| Measure | Value |
|---|---|
| Paraphrase recovery (no shared content word) | .667 |
| Coverage withheld on constructed non-correspondences | 72.3% |
| False-absence rate | .008 |
| Margin over embedding baseline | +22 pp (ARI .012) |
| Confidence separation, correct vs erroneous | .841 / .675 (AUROC .662) |
| Label reliability, Krippendorff's alpha | .580 [.518, .641] |

**Gap profile** (percentage of transposable requirement units):

| Jurisdiction | C1 | C2 | C3 | C4 | C5 |
|---|---|---|---|---|---|
| Bahrain | 9.9 | 35.7 | 9.4 | 26.3 | 18.7 |
| United Arab Emirates | 11.7 | 34.5 | 5.8 | 24.6 | 23.4 |
| Saudi Arabia | 8.2 | 46.8 | 8.2 | 19.3 | 17.5 |
| Oman | 7.0 | 39.2 | 11.7 | 22.2 | 19.9 |
| Qatar | 3.5 | 49.1 | 7.6 | 20.5 | 19.3 |
| Kuwait | 2.3 | 25.7 | 7.6 | 19.9 | 44.4 |
| **All** | **7.1** | **38.5** | **8.4** | **22.1** | **23.9** |

Partial coverage is modal in five of six jurisdictions. The characteristic divergence
is incompleteness rather than absence: the statutes identify the actor bound and the
consequence of breach while leaving the regulated conduct underspecified.

---

## Repository layout

```
notebooks/     Colab notebook, end to end
data/
  corpus/      Statute corpus and extraction quality
  instrument/  Requirement units, screening rule, excluded set
  reference_kb/Parsed reference text and leakage-guard self-test
  index/       FAISS index and embeddings
results/
  records/     Main run, stability replicates
  perturbations/ Mutations, negative controls, metamorphic
  ablation/    Five-configuration grid
  metrics/     Consolidated metrics and derived tables
  traces/      Every model call with prompt hash and output
figures/       All figures, PNG and vector PDF
paper/         Manuscript sections
docs/          Data dictionary, reproduction guide, evaluation protocol
```

See [`docs/DATA.md`](docs/DATA.md) for a file-by-file description and
[`docs/REPRODUCE.md`](docs/REPRODUCE.md) for reproduction instructions.

---

## Reproducing

Open `notebooks/gcc_gdpr_gap_analysis.ipynb` in Colab with a T4 runtime and run top to
bottom. Two API keys are required as Colab secrets: `OPENAI_API_KEY` and
`TOGETHER_API_KEY`.

The notebook is checkpointed throughout. Re-running skips completed work, so an
interrupted run resumes rather than restarting. To recompute metrics only, without
issuing any model call, run the setup cells and then section 16 onward against the
artefacts in `results/`.

---

## Evaluation without expert annotation

No annotated reference set exists for statutory gap analysis in any jurisdiction. The
protocol substitutes three sources of correctness, none requiring expert labelling:

- **Constructed oracles** — provisions are perturbed in ways that determine the
  required verdict (deletion, paraphrase, modal downgrade, scope change, slot deletion)
- **Distractor injection** — requirement units are paired with provisions retrieved for
  unrelated requirements, so absence is correct by construction
- **Metamorphic relations** — the verdict must be invariant under article renumbering,
  jurisdiction masking and permutation of candidate order

See [`docs/EVALUATION.md`](docs/EVALUATION.md).

---

## Limitations

Individual verdicts are moderately stable (alpha = .580); jurisdiction-level
percentages are more dependable than any single cell. Verdicts are sensitive to the
order in which candidate provisions are presented (.591 invariance, not distinguishable
from chance). Retrieval returned no candidates in 46 of 1,026 records, 45 of them
Kuwait, whose corpus comprises nine articles. The ablation does not isolate individual
component contributions at the available sample size.

---

## Citation

```bibtex
@article{gccgdpr2026,
  title   = {Metacognitive Multi-Agent Reasoning for Legal Gap Analysis in
             Low-Resource Cross-Jurisdictional Statutory Comparison},
  year    = {2026}
}
```

## Licence

Code: MIT ([`LICENSE`](LICENSE)). Data and figures: CC BY 4.0
([`LICENSE-DATA`](LICENSE-DATA)). Third-party reference documents are not
redistributed; see [`data/reference_kb/SOURCES.md`](data/reference_kb/SOURCES.md).
