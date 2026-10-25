# MAAI901 Applied Vision Transformer Report

## Project Overview
Fine-tuning a Vision Transformer (ViT-B/16) and ResNet-50 baseline for brain tumor MRI classification. 

## Repository Structure
- `notebooks/`: Contains the main Colab execution notebook.
- `checkpoints/`: Model weights and dataset split indices.
- `figures/`: Training curves, confusion matrices, and attention rollouts.
- `src/`: (Optional) Python scripts if refactoring from the notebook.

## Reproducibility
To reproduce this project:
1. Clone the repository.
2. Download the Kaggle dataset `masoudnickparvar/brain-tumor-mri-dataset`.
3. Run the top-to-bottom Colab notebook. The split seed is fixed to 42.
