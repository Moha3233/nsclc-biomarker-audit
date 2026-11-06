# Research Question

## Problem

Many published studies identify candidate cancer biomarkers using a similar
recipe: differentially expressed genes (DEGs), protein-protein interaction (PPI)
hub genes, and a machine learning filter, followed by a reported AUC. However,
AUC measures only how well a gene ranks cancer above normal samples. It does not
show that predicted probabilities are trustworthy (calibration), and it does not
show that the same genes would be selected again if the data changed slightly
(stability). These studies also often validate on small test sets, and some use
the test set to decide which genes qualify as biomarkers. It is therefore unclear
how reliable the reported biomarkers are.

## What I will do

I will audit published non-small cell lung cancer (NSCLC) biomarker studies that
use the DEG -> PPI -> machine learning recipe. I will:

1. Collect 15-30 such papers and record their reported gene signatures, datasets
   and claimed performance.
2. Re-evaluate every signature on independent public datasets (GEO and TCGA) that
   the paper did not use for training.
3. Compare each signature against random gene sets of the same size.
4. For papers whose pipelines are fully described, re-run the gene selection on
   bootstrap resamples of the training data to measure stability.

The starting paper is Rabby et al. (2025), PLoS ONE, which reports EDNRB and MME
as NSCLC biomarkers.

## What I will measure

- Discrimination: AUC with bootstrap 95% confidence intervals.
- Calibration: Brier score, calibration slope and intercept, expected calibration
  error (ECE), and reliability curves, before and after recalibration.
- Baseline: the percentile of each signature's AUC within the distribution of
  1,000 random gene sets of the same size.
- Cross-cohort transfer: performance when trained on one cohort and tested on a
  different one.
- Stability: the fraction of bootstrap resamples (n = 100) in which each reported
  gene is re-selected, and the overlap between signatures from different papers.

## What would count as a result

Claims hold if, on independent data, a signature keeps AUC above 0.90 with a
confidence interval that does not cross 0.80, shows acceptable calibration (slope
close to 1, low ECE), clearly outperforms random gene sets (above the 95th
percentile), and its genes are re-selected in most bootstrap resamples.

Claims do not hold if AUC drops substantially on independent data, calibration is
poor, random gene sets perform comparably, or reported genes are rarely
re-selected.

Either outcome is a valid finding. Mixed results (for example, good
discrimination but poor calibration) are also expected and will be reported by
signature and by pipeline step.

## Pre-specified limitations

- Public datasets are small and mostly microarray-based.
- Papers that do not describe their pipeline fully cannot be re-run, and this will
  be recorded as a finding rather than excluded silently.
- Results apply to tissue-versus-normal NSCLC diagnosis only, not to other cancers
  or to prognosis.
