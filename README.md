# ECG-TransNet: Multi-Dataset CNN–Transformer Framework for Arrhythmia Detection

> A hybrid **1D-CNN + Transformer** framework for ECG arrhythmia classification, combining morphological feature extraction with temporal sequence modeling.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-ee4c2c)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## Overview

**ECG-TransNet** is a research project for automated ECG arrhythmia classification using a hybrid deep learning architecture.

The model combines:

* **1D Convolutional Neural Networks** for local ECG morphology
* **Transformer encoders** for temporal and contextual dependencies
* **Explainable AI** techniques for model interpretation
* **Class-imbalance handling** for underrepresented arrhythmia categories

The project is designed around the **AAMI EC57** classification framework and uses ECG data from the **MIT-BIH Arrhythmia Database**.

### Research Status

✅ Model and experiments completed
📄 Currently being prepared for conference submission

---

## Motivation

ECG signals contain information at multiple temporal scales.

Short local patterns can indicate morphological abnormalities, while relationships between successive heartbeats can provide important rhythm information.

ECG-TransNet therefore combines two complementary modeling approaches:

**CNN → Morphology**

Learns local waveform characteristics such as QRS morphology, ST-segment changes, and T-wave patterns.

**Transformer → Temporal Context**

Models relationships between multiple heartbeat segments, including rhythm variability and beat-to-beat dependencies.

The overall idea is:

```text
ECG Signal
    ↓
Preprocessing
    ↓
1D CNN Feature Extraction
    ↓
Transformer Temporal Modeling
    ↓
Classification Head
    ↓
Arrhythmia Class
```

---

## Model Architecture

### 1. CNN Feature Encoder

The convolutional front-end extracts local features from the ECG waveform.

Its role is to capture morphological patterns that distinguish different heartbeat classes.

### 2. Transformer Encoder

The extracted representations are passed to Transformer layers using multi-head self-attention.

This allows the model to capture relationships across different portions of the ECG sequence rather than treating each local pattern independently.

### 3. Classification

The learned representation is aggregated and passed through a classification head to predict the target arrhythmia category.

---

## Explainability

The project includes explainability methods to investigate which regions of an ECG signal contribute to model predictions.

Current methods include:

* **Grad-CAM** — visualization of activation-based importance
* **SHAP** — feature-attribution analysis

These methods are intended to make model decisions easier to inspect and analyze during research.

---

## Dataset

The project uses the **MIT-BIH Arrhythmia Database** and follows the AAMI-based beat classification framework.

| Class | Description                    |
| ----- | ------------------------------ |
| **N** | Normal and related beats       |
| **S** | Supraventricular ectopic beats |
| **V** | Ventricular ectopic beats      |
| **F** | Fusion beats                   |
| **Q** | Unknown / paced / other beats  |

### Preprocessing Pipeline

```text
Raw ECG
  ↓
Band-pass filtering
  ↓
Baseline/noise processing
  ↓
Normalization
  ↓
R-peak / beat detection
  ↓
Beat-centered segmentation
  ↓
Model input
```

The current preprocessing pipeline includes Butterworth filtering, normalization, and beat-centered segmentation.

---

## Handling Class Imbalance

Arrhythmia datasets are typically highly imbalanced, with normal beats substantially more common than several abnormal classes.

The project therefore includes techniques such as:

* Weighted cross-entropy
* Data augmentation
* AAMI-based class organization
* Class-wise evaluation metrics

The goal is to prevent the model from being dominated by the majority class.

---

## Reported Results

The current project reports the following experimental results:

| Metric               |   Result |
| -------------------- | -------: |
| Overall Accuracy     |   ~98.2% |
| Average F1-Score     |    ~0.94 |
| Inference Latency    |  < 12 ms |
| Quantized Model Size | ~27.4 MB |

These values represent the current project benchmarks and should be interpreted together with the corresponding experimental setup and evaluation protocol.

---

## Repository Structure

```text
ECG-TransNet/
│
├── data/                       # Dataset and processed data
├── preprocessing/              # ECG signal preprocessing
│
├── models/                     # Model implementations
│   ├── cnn_encoder.py
│   ├── transformer.py
│   └── ecg_transnet.py
│
├── training/                   # Training and evaluation
│   ├── train.py
│   └── evaluate.py
│
├── interpretability/           # Explainability methods
│   ├── gradcam.py
│   └── shap_analysis.py
│
├── results/                    # Generated results and visualizations
│
├── requirements.txt
└── README.md
```

---

## Installation

### Clone the repository

```bash
git clone https://github.com/PeerAhammad/ECG-TransNet-Arrhythmia-Detection.git
cd ECG-TransNet-Arrhythmia-Detection
```

### Install dependencies

```bash
pip install -r requirements.txt
```

---

## Training

Example training command:

```bash
python training/train.py --config configs/production_run.yaml
```

---

## Model Evaluation

```bash
python training/evaluate.py
```

---

## Explainability

### Grad-CAM

```bash
python interpretability/gradcam.py --sample_id 100_beat_5
```

### SHAP

```bash
python interpretability/shap_analysis.py
```

---

## Research Focus

This project explores the intersection of:

* ECG signal processing
* Deep learning
* Transformer architectures
* Time-series classification
* Medical AI
* Explainable AI
* Imbalanced learning

---

## Future Work

Potential extensions include:

* Evaluation across additional ECG datasets
* Further cross-dataset generalization experiments
* Improved explainability evaluation
* Model calibration and uncertainty estimation
* Additional efficiency and deployment experiments
* Conference submission and peer review

---

## Dataset Reference

The project uses the **MIT-BIH Arrhythmia Database** provided through PhysioNet.

**MIT-BIH Arrhythmia Database**
Moody GB, Mark RG.

**PhysioBank / PhysioToolkit / PhysioNet**
Goldberger AL et al.

Dataset DOI:

[10.13026/C2F305](https://doi.org/10.13026/C2F305)

---

## Project Status

**Current status: Completed research project**

The core model, experiments, evaluation, and explainability components have been developed. The project is currently being prepared for submission to a suitable research conference.

---

## License

This project is released under the **MIT License**.
