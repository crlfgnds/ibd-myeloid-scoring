# IBD Myeloid Scoring

Predicting IBD diagnosis and subtype (Crohn's vs UC) from myeloid inflammatory gene program scores in bulk ileal RNA-seq data (GSE137344).

## Setup
```bash
conda env create -f environment.yml
conda activate ibd-myeloid
```

## Project Structure

- `src/` — Python scripts
- `notebooks/` — Jupyter notebooks for exploration
- `config/` — gene signatures and parameters
- `data/` — raw and processed data (not tracked by git)
- `tests/` — unit tests
- `figures/` — saved plots

## Author
Anna Fagundes
