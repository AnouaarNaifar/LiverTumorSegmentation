# Tumor and Liver Segmentation

Deep-learning experiments for segmenting liver and liver tumors in 3D CT scans. The project compares a direct multiclass U-Net with two-stage pipelines, with and without attention gates.

## Experiment tracks

| Track | Notebook | Purpose |
| --- | --- | --- |
| Two-stage with attention | `ATTENTION_NO_FINETUNING/améiloration_fixed_attention_no_finetuning.ipynb` | Detect the liver, then detect tumors inside the liver with attention gates. |
| Multiclass | `MULTI_CLASS/multiclass_fine_tuning fixed.ipynb` | Predict background, liver, and tumor labels in one pass. |
| Two-stage without attention | `no_attention/améiloration_fixed_no_attention.ipynb` | Baseline liver-then-tumor pipeline without attention gates. |

The `extract.ipynb` notebooks contain supporting extraction or inspection steps. Notebook names and paths are preserved from the working project so previous experiment references remain recognizable.

## Dataset

The LiTS dataset is not stored in this repository. Download it from the [LiTS Kaggle mirror](https://www.kaggle.com/datasets/andrewmvd/liver-tumor-segmentation) or another authorized source, then arrange it like this:

```text
dataset/
├── volume_pt1/
│   ├── volume-0.nii
│   └── ...
├── volume_pt2/
├── volume_pt3/
├── volume_pt4/
├── volume_pt5/
├── volume_pt6/
├── volume_pt8/
└── segmentations/
    ├── segmentation-0.nii
    └── ...
```

The notebooks pair `volume-<id>.nii` with `segmentation-<id>.nii`. Update the dataset path in the data-loading cells for your machine. The data and model files are intentionally ignored by Git because they are very large and may be subject to dataset licensing terms.

## Setup

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
jupyter notebook
```

For GPU training, install the PyTorch packages matching your CUDA version using the official PyTorch installation selector before installing the remaining requirements.

Run a notebook from top to bottom. A typical workflow is:

1. Configure imports and paths.
2. Discover and visualize the dataset.
3. Build preprocessing, model, loss, and dataloader components.
4. Train or load a checkpoint.
5. Run inference and evaluate the predictions.

## Repository policy

Tracked files contain source notebooks, lightweight configuration, and documentation. The following remain local and are excluded from commits:

- LiTS NIfTI volumes and other medical-imaging data
- model checkpoints and training archives
- generated outputs, captures, and notebook exports
- Python environments, caches, and editor settings

This is a research and educational project, not a clinically validated diagnostic system.

## GitHub setup

Create an empty repository under your own GitHub account, then run:

```powershell
git init
git add .
git commit -m "Initial project snapshot"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repository>.git
git push -u origin main
```

Do not commit the dataset or checkpoints. GitHub rejects files above its size limits, and the dataset may have separate redistribution restrictions.
