# IBD Myeloid Scoring

Predicting Crohn's disease diagnosis from myeloid inflammatory gene program scores in bulk ileal RNA-seq data — using cell-type signatures derived from single-cell RNA-seq as interpretable features for classification.

**Logistic Regression ROC-AUC: 0.81 | 12 features | 1,618 samples**

---

## Background

Inflammatory bowel disease (IBD) comprises Crohn's disease (CD) and ulcerative colitis (UC), conditions driven in part by dysregulated myeloid cell activity in the gut mucosa. While bulk RNA-seq remains the most scalable transcriptomic readout in clinical settings, it obscures cell-type-specific signals.

This project tests whether myeloid inflammatory programs — derived from single-cell data — can be projected back onto bulk tissue to yield biologically interpretable features capable of predicting IBD diagnosis.

---

## Approach

```
scRNA-seq (myeloid cells)
        │
        ▼
Wilcoxon marker gene extraction
(12 cell types: macrophages, neutrophils, DCs, monocytes)
        │
        ▼
Bulk RNA-seq (GSE193677, ileal biopsies)
        │
        ▼
DESeq2 differential expression (CD vs control)
        │
        ▼
Mean-based signature scoring
(1,618 samples × 12 myeloid program scores)
        │
        ▼
Classification: Logistic Regression + Random Forest
```

---

## Results

| Model               | ROC-AUC | Accuracy | F1 (CD) | F1 (Control) |
|---------------------|---------|----------|---------|--------------|
| Logistic Regression | **0.81**| 73%      | 0.84    | 0.27         |
| Random Forest       | 0.72    | 74%      | 0.84    | 0.35         |

Both models were trained on 1,294 samples and evaluated on 324 held-out samples. The dataset is imbalanced (71.5% CD, 28.5% control), which limits recall on the minority class — addressed in `notebooks/07_modeling.ipynb`.

![ROC curve - Logistic Regression](figures/roc_auc_logistic.png)
![ROC curve - Random Forest](figures/roc_auc_forest.png)

---

## Dataset

**GSE193677** — bulk ileal RNA-seq from IBD patient biopsies (GEO, public).  
1,618 samples: Crohn's disease (n≈1,157) and non-IBD controls (n≈461).  
Raw counts processed via DESeq2; 40,317 genes mapped from ENSEMBL to gene symbols.

---

## Setup

```bash
conda env create -f environment.yml
conda activate ibd-myeloid
```

---

## Repository Structure

```
├── config/          # gene signatures and analysis parameters
├── notebooks/       # analysis pipeline (01–07, sequential)
│   ├── 01_exploration.ipynb
│   ├── 02_scrna_preprocessing.ipynb
│   ├── 03_scrna_dimreduction.ipynb
│   ├── 04_scrna_reclustering.ipynb
│   ├── 05_scrna_signature_extraction.ipynb
│   ├── 06_scoring_bulk_seq.ipynb
│   └── 07_modeling.ipynb
├── src/             # scoring.py, scrna.py modules
├── tests/           # unit tests
├── figures/         # saved plots
└── data/            # raw and processed data (not tracked)
```

---

## Author

Anna Fagundes — PhD, Computational Immunology  
[github.com/crlfgnds](https://github.com/crlfgnds)
