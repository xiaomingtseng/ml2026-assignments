# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Environment Setup

This project uses [uv](https://docs.astral.sh/uv/) as the package manager with Python 3.12+.

```powershell
# Install dependencies (creates/syncs .venv)
uv sync

# Run a notebook
uv run jupyter notebook a3_common.ipynb

# Run a Python script
uv run python a3_common.py
```

PyTorch is installed with CUDA 12.1 support via the `pytorch-cuda-12.1` index in `pyproject.toml`.

## Architecture

This is a coursework ML assignments repository (2026) with shared utility modules designed for team collaboration. Each team member imports from the common modules and adds their own model implementations.

### Assignment 3 — Classical ML (`a3_common.ipynb`)

- **Dataset:** UCI Sonar (208 samples, 60 features, binary classification via `ucimlrepo`)
- **Pattern:** Nested cross-validation with `RepeatedStratifiedKFold(n_splits=5, n_repeats=5)` outer CV and `GridSearchCV` inner CV
- **Key functions:**
  - `run_model(name, pipeline, param_grid, inner_cv=3)` — runs nested CV and returns results dict with mean±std for accuracy, precision, recall, F1, ROC-AUC
  - `show_results(results_list)` — formats and displays a comparison table
  - `plot_confusion_matrix(model_name, pipeline, param_grid)` — fits best model and plots CM
- **`RANDOM_SEED = 2026`** is used globally for reproducibility

### Assignment 4 — Deep Learning (`a4_common.ipynb`)

- **Dataset:** Meta-Album PLK Micro (OpenML ID 44238) — plankton image classification, auto-downloaded
- **Two approaches supported:**
  1. Classical ML: `make_pixel_features(df, size, grayscale)` flattens images for sklearn pipelines
  2. Deep Learning: `PlanktonDataset` (PyTorch `Dataset`) + `make_loaders(train_tf, eval_tf, ...)`
- **Key functions:**
  - `make_loaders(train_tf, eval_tf, batch_train, batch_eval)` — returns `(train_loader, val_loader, test_loader)` with 60/20/20 stratified split
  - `train_model(model, train_loader, val_loader, epochs, lr, weight_decay)` — full training loop, returns history dict
  - `evaluate(model, loader, criterion)` — returns `(loss, accuracy, macro_f1, all_preds, all_labels)`
  - `plot_learning_curves(history, model_name)` — plots train/val loss and accuracy
- **Transform presets:** `cnn_train_tf`/`cnn_eval_tf` use 128×128; `resnet_train_tf`/`resnet_eval_tf` use 224×224 with ImageNet normalization
- **Device:** `device = torch.device("cuda" if torch.cuda.is_available() else "cpu")` auto-detected
- **`RANDOM_SEED = 2026`**, `IMG_SIZE_CNN = 128`, `IMG_SIZE_RES = 224`
- **Image loading:** uses OpenML cache (`openml.config.get_cache_directory()/datasets/44238/`) + `X_meta` metadata for authoritative path→label mapping

### Notes

- Comments in the notebooks are written in Traditional Chinese (繁體中文).
- The `.ipynb` files are the primary working surfaces for assignments.
