# Project Setup Cheatsheet

## One-time setup (already done)

### 1. Create conda environment
conda create -n ibd-myeloid python=3.11 -y

### 2. Activate environment
conda activate ibd-myeloid
# Do this every time you open a new terminal

### 3. Install packages
conda install -c conda-forge pandas numpy matplotlib jupyter ipykernel -y
pip install ruff pre-commit

### 4. Export environment (do this after every new install)
conda env export --no-builds | grep -v "^prefix:" > environment.yml

### 5. VS Code extensions (already installed)
code --install-extension ms-python.python
code --install-extension ms-toolsai.jupyter
code --install-extension charliermarsh.ruff

## Daily workflow

### Start working
cd ~/ibd-myeloid-scoring
conda activate ibd-myeloid
code .

### Save your work to GitHub
git add .
git commit -m "describe what you did"
git push

### Check status
git status
git log --oneline
