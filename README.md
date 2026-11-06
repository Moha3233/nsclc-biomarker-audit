# nsclc-biomarker-audit

# NSCLC Biomarker Audit

A calibration and stability benchmark for bioinformatics biomarker pipelines, applied to published non-small cell lung cancer (NSCLC) hub-gene biomarker studies.

> **Status:** Early stage (Phase 0: setup). No results yet.

## Research question

Do gene biomarkers reported by published "DEG → PPI hub gene → machine learning" studies of NSCLC remain well calibrated, discriminative and stable when re-tested on independent public datasets?

## Motivation

Many studies identify candidate biomarkers with a similar recipe: differential expression, protein-protein interaction (PPI) hub genes, and a machine learning filter, and then report an AUC. Discrimination (AUC) alone does not show that predicted probabilities are trustworthy, and selected genes can change with small changes in the data. This project audits those claims systematically instead of proposing new biomarkers.

The starting paper is Rabby et al. (2025), *PLoS ONE* 20(2): e0317296, which reports EDNRB and MME as NSCLC biomarkers.

## Approach

1. **Corpus:** collect published NSCLC biomarker papers and record their gene signatures, datasets and claimed performance (`data/corpus.csv`).
2. **Independent data:** assemble public datasets (GEO, TCGA) that none of the audited papers used for training.
3. **Fixed evaluation protocol** (written before running analyses, see `docs/PROTOCOL.md`):
   - Discrimination: AUC with bootstrap confidence intervals
   - Calibration: Brier score, calibration slope/intercept, expected calibration error, reliability curves
   - Baselines: random gene sets of matching size
   - Cross-cohort transfer
4. **Stability:** re-run selection steps on bootstrap resamples and measure how often reported genes are re-selected.
5. **Report:** preprint plus journal submission.

## Repository structure

```
data/
  raw/            # downloaded by script, not tracked by git
  processed/      # cleaned expression matrices
  corpus.csv      # papers and reported signatures
docs/
  QUESTION.md     # research question
  PROTOCOL.md     # pre-specified analysis plan
notebooks/        # exploratory analysis
src/              # R and Python scripts
results/          # tables and figures
```

## Reproducibility

- All data come from public sources (GEO, TCGA) and are downloaded by script using accession numbers.
- Environment: `environment.yml` (to be added).
- Planned: one-command workflow (Snakemake or Makefile) and a Zenodo archive for a citable DOI.

## Getting started

```bash
git clone https://github.com/[your-username]/nsclc-biomarker-audit.git
cd nsclc-biomarker-audit
# environment setup instructions will be added here
```

## Roadmap

- [ ] Phase 0: Repo and environment setup
- [ ] Phase 1: Build paper corpus (15-30 papers)
- [ ] Phase 2: Assemble independent validation datasets
- [ ] Phase 3: Reproduce the starting paper
- [ ] Phase 4: Calibration and baseline audit
- [ ] Phase 5: Stability analysis
- [ ] Phase 6: Preprint and submission

## Author

[Your name]

## License

MIT License. See `LICENSE`.

## Reference

Rabby MS, Islam MM, Kumar S, Maniruzzaman M, Hasan MAM, Tomioka Y, Shin J. Identification of potential biomarkers for lung cancer using integrated bioinformatics and machine learning approaches. PLoS ONE. 2025;20(2):e0317296. https://doi.org/10.1371/journal.pone.0317296
