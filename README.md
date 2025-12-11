# Bartangi Pipeline (v1.0)

Reproducible Bartangi NLP pipeline: rules+exceptions lemmatizer → cleaned lemmas → Word2Vec CBOW/SG embeddings → intrinsic + downstream evaluation.

[Zenodo DOI](https://zenodo.org/records/17836415)

## Reproduce (Colab/local)
- Python 3.10+, `gensim==4.*`, `scikit-learn`, `pandas`, `numpy`, `pyyaml`.
- Run in order:
  1. `scripts/00_normalize_dedup.py` → writes `data/raw_corpus.txt` and `artifacts/stats/corpus_stats.csv`
  2. `scripts/01_lemmatize_rules.py` → writes `artifacts/lemmas.txt`
  3. `scripts/02_train_w2v.py` → saves `models/w2v_cbow.model`, `models/w2v_sg.model`
  4. `scripts/03_eval_doccls.py` → writes `results/downstream_results.csv`, `results/ablation.csv`
  5. `scripts/04_intrinsic_score.py` (uses `gold/lemma_gold_review.csv`) → prints lemmatizer accuracy

**Final numbers (3-seed average):**
- CBOW: **0.5361 macro-F1 / 0.5389 acc**
- Skip-gram: **0.5206 / 0.5222**
- Ablation (raw→lemma, CBOW): **+0.0211 F1 / +0.0222 acc**
- Intrinsic lemmatizer (300 tokens, 53 changed): **99.33%**

## Licensing / Provenance
We redistribute **derived artifacts** (lemmas, rules, embeddings, results, figures). Raw sources are not republished. See `artifacts/stats/provenance.csv`.
License: MIT.
