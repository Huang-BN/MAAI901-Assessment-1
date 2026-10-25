# MAAI901 Applied Vision Transformer Report

Individual assessment for MAAI901 - Deep Learning for Visual Data (Master of Applied Artificial Intelligence, UOWD).
Author: Bin Huang (8391865)

## Project Overview

This project applies a state-of-the-art Vision Transformer to a medical imaging task and compares it against a strong CNN baseline.

Task: Four-way classification of brain MRI slices into glioma, meningioma, pituitary, and no tumor.

Models:
- Baseline: ResNet-50 (ImageNet-1k pretrained)
- Main model: ViT-B/16 (google/vit-base-patch16-224-in21k)

For both models, the original classification head was replaced with a 4-unit linear layer, and both were trained on the identical stratified split.

Key findings:
- Both models achieved 98.33% accuracy and 0.9834 macro-F1 on the 720-image test set (12 errors each).
- On the clinically critical metric of false negatives, the ViT was marginally safer (2 vs 3 missed tumors).
- ResNet-50 was better calibrated (ECE 0.0100 vs 0.0208; Brier 0.0248 vs 0.0263).
- Attention rollout revealed shortcut learning: the ViT attended to skull and background artifacts rather than tumor tissue.
- The dataset lacks patient-level identifiers, so image-level splitting causes data leakage; the reported accuracy is therefore inflated and neither model is clinically deployable.

Full analysis, discussion of biases, and ethical implications are in the report.

## Repository Structure

- notebooks/: Contains the main Colab execution notebook.
- figures/: Training curves, confusion matrices, and attention rollouts.
- checkpoints/: Dataset split indices (dataset_splits.json).
- Report-and-Presentation/: Final PDF report and slide deck.

The fine-tuned checkpoints (resnet50_best.pth, vit_best.pth) and the Kaggle dataset are not committed to this repository. See below for how to obtain or regenerate them.

## Dataset

The dataset is not included in this repository. Download it from Kaggle:
- Name: masoudnickparvar/brain-tumor-mri-dataset
- URL: https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset
- Size: about 150 MB, 7,200 images, 4 classes, perfectly balanced (1,800 per class)

The notebook downloads it automatically via the Kaggle API. You must supply your own Kaggle API token (kaggle.json); instructions are in the first cell of the notebook.

## Trained Weights

The fine-tuned checkpoints are not committed to the repository.
Regenerate them by running the notebook top-to-bottom on a Colab T4 GPU. Training takes approximately 30 to 60 minutes.

The reproducible dataset split is committed as checkpoints/dataset_splits.json (seed = 42), so training is deterministic given the same environment.

## How to Reproduce

Google Colab (recommended):
1. Open notebooks/MAAI901.ipynb in Google Colab.
2. Set the runtime to GPU T4 (Runtime, Change runtime type).
3. Upload your kaggle.json when prompted.
4. Run all cells top-to-bottom.
5. All figures are saved to figures/; the best checkpoints are saved during training.

## Environment

- Hardware: Google Colab, NVIDIA T4 GPU
- Python: 3.10+
- Key libraries: PyTorch, torchvision, Hugging Face Transformers, scikit-learn, matplotlib, seaborn, OpenCV, tqdm, Pillow
- Pinned versions: see requirements.txt

## Declaration of Generative AI Use

The generative AI tools Claude and Gemini were accessed between 16 October 2026 and 25 October 2026 to assist in the writing, editing, and formulation of the MAAI901 assessment task, Applied Vision Transformer Report.

First, the tools were used to help draft and proofread the prose of this report. All technical content, figures, tables, and numerical results are my own, as are the analysis, findings, and critical decisions made throughout the project. Every line of the report was reviewed, validated, and edited by me.

Second, the tools assisted with generating repetitive code in my Colab notebook, for example the standard PyTorch training loop, the DataLoader setup, and the attention-rollout helper function. I verified, adapted, and tested all generated code against my own data and corrected errors.

Third, the tools were used to debug and fix runtime errors, for example the Hugging Face eager-attention setting and the OpenCV float16-to-float32 type conversion. The fixes were implemented and validated by me.

Bin Huang - bh329@uowmail.edu.au - Student ID 8391865
