# custom-cnn-inception-weight-initialization
Image classification experiments comparing custom CNNs, Inception-style networks, and baseline-trained weight initialization.

# Question
Does training a custom CNN first give a better initialization for an Inception-style network?

This project tests that question empirically.

# Experiments

Custom CNN baseline — random initialization, trained from scratch.
Inception-style model — random initialization, trained from scratch.
Inception-style model with baseline initialization — compatible weights from the trained baseline are copied into explicitly shared layers.
ImageNet-pretrained InceptionV3 — separate conventional transfer-learning reference.
The custom CNN → Inception-style experiment is called weight initialization, not standard transfer learning.

# Experimental Design

For a fair comparison, keep the following consistent:

Dataset split
Preprocessing
Data augmentation
Batch size
Training budget
Evaluation metrics
Comparable optimizer/learning-rate settings
Prefer multiple runs with controlled random seeds before drawing conclusions.

# Metrics

Compare:

Accuracy
Precision
Recall
F1-score
ROC-AUC when appropriate
Training/validation loss
Convergence speed
Trainable parameter count
Training time

# Repository Structure

image_classification/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── image_classification.ipynb
├── models/
│   ├── base_model.py
│   ├── inception_model.py
│   └── weight_transfer.py
├── weights/
│   └── .gitkeep
└── results/
    └── .gitkeep

# Installation

git clone <YOUR_REPOSITORY_URL>
cd image_classification
pip install -r requirements.txt

Open notebooks/image_classification.ipynb and configure the dataset and data_agg augmentation pipeline.
Saving and Loading Weights
model.save_weights("weights/base_model.weights.h5")
Recreate the same architecture before loading:
model.load_weights("weights/base_model.weights.h5")
Large checkpoints are excluded from Git.
Weight Initialization
Weights are copied only between explicitly matched layers with identical weight shapes. Target-only layers remain randomly initialized.
This prevents accidental or invalid checkpoint loading between incompatible architectures.

# Status

Experimental / learning project. Results should be interpreted as empirical findings for this dataset and setup, not as universal claims about architectures or initialization methods.
