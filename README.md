
# Lane Detection and Driver Assistance

This project collects the materials and results for a lane detection system
designed to identify lane markings and produce clear lane overlays that can be
used in driver-assistance demonstrations. The repository contains the LaTeX
report source and a set of illustrative images showing dataset samples,
preprocessing steps, the model architecture (U‑Net), and prediction overlays.

Why this project
-----------------
Accurately detecting lane markings is a fundamental task for many advanced
driver assistance systems. This work explores a segmentation-based approach to
detect lane regions robustly, examines preprocessing choices, and reports
quantitative and qualitative results that show the model's strengths and
limitations on sample data.

What you'll find here
---------------------
- `main.tex` — The LaTeX source document containing the full report and figures.
- `images/` — Visual assets used in the report (dataset samples, masks,
  overlays, architecture diagrams, training/validation plots, and more).

Project highlights
------------------
- Model: U‑Net style segmentation network adapted for lane detection.
- Preprocessing: Color-space normalization, resizing, and optional augmentation
  (horizontal flips, brightness/contrast jitter, random crops).
- Training: Supervised segmentation with binary / dice-style loss and data
  augmentation. Training observations and sample learning curves are in the
  report images.
- Outputs: Same-resolution mask predictions and overlay visualizations that
  blend predicted lanes with the original images for easy inspection.

Dataset and annotations
-----------------------
The images in `images/` include both raw samples and example ground-truth
masks used during training/validation. The report explains dataset statistics
and how masks were generated or cleaned for training.

Method overview
---------------
1. Preprocessing: Resize images to a fixed training resolution, normalize pixel
   intensities, and apply data augmentation to increase robustness.
2. Model: U‑Net encoder–decoder architecture with skip connections to preserve
   spatial detail. The final layer produces a single-channel probability map for
   lane vs. background.
3. Loss: Combination of Binary Cross-Entropy and Dice (or IoU) loss to handle
   class imbalance and encourage mask overlap.
4. Postprocessing: Threshold probabilities, perform morphological cleanup (open/close),
   and optionally fit polynomial lanes for geometric smoothing.

Training details (example)
--------------------------
- Optimizer: AdamW or Adam
- Learning rate: 1e-4 (with cosine/step scheduling)
- Batch size: depends on GPU memory (typical: 8–16)
- Epochs: 30–100 (monitor val loss / IoU)
- Regularization: weight decay, dropout in decoder as needed

Evaluation and results
----------------------
Evaluation uses pixel-level metrics (IoU, Dice) and qualitative overlays to
measure both numerical performance and how the model behaves on edge cases
(shadows, occlusions, worn lane markings). The report contains plots and
example outputs; see `images/` for sample overlays and mask comparisons.

Demo / visualization
--------------------
The repository includes images showing a simple demo interface (see
`images/web_interface.png`). A lightweight demo can load a trained model,
run inference on new frames, and display the original image with a colored
overlay for predicted lanes.

How to reproduce (short)
------------------------
1. Prepare a Python environment with the usual ML stack (PyTorch, torchvision,
   OpenCV, NumPy, Matplotlib).
2. Place training images and masks in the expected folders and update any
   path variables in the training script.
3. Train with the hyperparameters above; save model checkpoints and export a
   final inference script for producing overlays.

Files in this repo
------------------
- `main.tex` — Full written report (compile to get the PDF).
- `images/` — All figures referenced in the report.
