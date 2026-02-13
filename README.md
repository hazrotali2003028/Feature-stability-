# Stability-Driven Seizure Detection: Ensemble Feature Voting for Epilepsy

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![Status](https://img.shields.io/badge/Status-Research_Preprint-orange)]()
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

## 📌 Overview
**Project Title:** Addressing Feature Instability in Small-Sample Epilepsy Datasets using Ensemble Feature Voting

This repository contains the implementation of a novel **Ensemble Feature Voting** framework designed to solve the "Stability-Performance Trade-off" in EEG-based seizure detection. 

While traditional machine learning models often achieve high accuracy (~90%) on small datasets, they frequently suffer from **model fragility** (low Jaccard Index), selecting different features every time the data is shuffled. This work proposes a mathematical consensus mechanism to identify **invariant physiological biomarkers** that remain stable across diverse patient cohorts.

## 🔬 Key Contributions
* **Problem Identified:** Standard Random Forest pipelines exhibited severe instability ($J=0.24$), proving they overfit to noise rather than signal.
* **Solution:** Introduced a **50-bootstrap Ensemble Voting** mechanism with an 80% consensus threshold.
* **Result:** Achieved **Perfect Feature Stability ($J=1.0$)** while maintaining high accuracy (**86.09%**).
* [cite_start]**Biomarker Discovery:** Identified **Permutation Entropy** at electrodes **Pz, C4, and F8** as the most robust indicators of epileptic activity[cite: 391, 411].

## 📂 Repository Structure
| File/Folder | Description |
| :--- | :--- |
| `preprocessing.ipynb` | [cite_start]**Step 1:** Raw EEG cleaning (Bandpass 0.5-45Hz, ICA Artifact Removal, AutoReject)[cite: 289]. |
| `feature_extraction.py` | [cite_start]**Step 2:** Extraction of 1,302 features (Spectral Power, Permutation Entropy, HFD, wPLI2 Connectivity)[cite: 278]. |
| `ensemble_voting.ipynb` | **Step 3:** The core logic. Runs 50 bootstrap iterations to calculate Jaccard Index and filter unstable features. |
| `results/` | Contains the Jaccard Stability heatmaps and Feature Importance plots. |

## 📊 Dataset
[cite_start]This study utilizes the **Mount Adora Epilepsy EEG Dataset**[cite: 228, 284].
* **Population:** 212 Subjects (110 Epileptic, 102 Normal).
* **Format:** 23-channel EEG (128 Hz sampling rate).
* **Preprocessing:** ICA cleaned, segmented into 4-second epochs.
* **Source:** [Mount Adora Epilepsy EEG Dataset](https://doi.org/10.5281/zenodo.13626065)

## 📈 Results: The Stability Gap
We compared a standard baseline model against our proposed ensemble framework.

| Metric | Baseline (Random Forest) | **Proposed Ensemble Voting** |
| :--- | :--- | :--- |
| **Accuracy** | 82.8% | **86.09%** |
| **Jaccard Index (Stability)** | 0.24 (Unstable) | **1.0 (Perfect Stability)** |
| **Top Feature** | Varied across folds | **Permutation Entropy (Pz)** |

> **Visual Proof:** The heatmaps below show how the baseline model (left) selects scattered, random features, while our method (right) converges on a stable set.

*(Note: Add your `image_ccda87.png` or stability heatmap images here in the repo)*

## 🛠️ Methodology
1.  **Preprocessing:** Downsampling (128Hz) -> Bandpass (0.5-45Hz) -> Average Reference -> ICA.
2.  **Feature Engineering:** Extracted **1,302 features** focusing on Non-linear Complexity (Higuchi Fractal Dimension, Permutation Entropy).
3.  **Ensemble Voting:**
    * Generate 50 bootstrapped subsets of data.
    * Train Random Forest on each subset.
    * **Vote:** Retain only features selected in $\ge 80\%$ of iterations.
    * **Validate:** Calculate Jaccard Index ($J$) to measure overlap.

## 🚀 Usage
1.  Clone the repo:
    ```bash
    git clone [https://github.com/HazrotAli/Epilepsy-Feature-Stability.git](https://github.com/HazrotAli/Epilepsy-Feature-Stability.git)
    ```
2.  Install dependencies:
    ```bash
    pip install mne numpy scikit-learn scipy matplotlib seaborn
    ```
3.  Run the voting mechanism:
    ```bash
    python ensemble_voting.py --bootstraps 50 --threshold 0.8
    ```

## 📝 Citation
This work is currently under review. If you utilize this code or the specific voting methodology, please cite this repository:

```bibtex
@misc{ali2026stability,
  title={Addressing Feature Instability in Small-Sample Epilepsy Datasets using Ensemble Feature Voting},
  author={Ali, Hazrot},
  year={2026},
  publisher={GitHub},
  journal={Work in Progress},
  howpublished={\url{[https://github.com/HazrotAli/Epilepsy-Feature-Stability](https://github.com/HazrotAli/Epilepsy-Feature-Stability)}}
}
