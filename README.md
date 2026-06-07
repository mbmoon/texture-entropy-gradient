# Robust Hyperspectral Image Classification: TEG-XGBoost vs 3D-CNN

## 📌 1. Overview
This repository contains the experimental Jupyter Notebook for evaluating the **Texture-Entropy-Gradient (TEG)** descriptor paired with an XGBoost classifier. The project benchmarks this proposed lightweight framework against a state-of-the-art deep learning architecture (Shallow 3D-CNN by Li et al., 2017) using the high-resolution **Pavia University** hyperspectral dataset. 

The primary focus of this research is to evaluate algorithmic stability under severe **Salt-and-Pepper (impulse) noise** and computational efficiency in a few-shot learning scenario (utilizing only 1% to 10% of training data).

## ⚙️ 2. Core Pipeline & Features
The notebook is structured to run end-to-end experiments, encompassing data degradation, feature extraction, and model benchmarking:
* **Impulse Noise Simulation:** Dynamically corrupts the hyperspectral cube with extreme sparsity noise ranging from 0% (clean) up to 20%.
* **Deterministic Feature Extraction (TEG):** Avoids deep convolutional pooling to prevent spatial noise blurring. It utilizes the Sobel operator (micro-edges), Local Entropy (spatial disorder), and multi-scale LBP. 
* **Dual Execution Modes:** * `Light Mode` (18 features): Ultra-fast processing using a pseudo-RGB composite + TEG.
  * `Heavy Mode` (618 features): Full spectral depth (103 channels) + TEG for maximum accuracy.
* **Hardware-Optimized Baseline:** The PyTorch 3D-CNN baseline includes dynamic memory clearing and supports CUDA, CPU, and Apple Silicon (MPS).

## 🚀 3. Experimental Setup & Benchmarking
The script automates the generation of learning curves and performance tables. For each noise level, it evaluates both models across varying training data fractions (1%, 5%, 10%, 20%, 50%, 70%). 
The benchmarking suite profiles:
1. **F1-Macro Score** and **Overall Accuracy (OA)**.
2. **Computational Profiling:** Precise tracking of feature extraction, model training, and full-scene inference times.
3. **Visual Classification Maps:** Generates masked and full-scene prediction plots alongside the expert ground truth.

## 📊 4. Key Findings
* **Noise Isolation:** While convolutional kernels in the 3D-CNN smear impulsive outliers across adjacent pixels leading to severe accuracy drops at 5%+ noise, the TEG-XGBoost ensemble successfully isolates these anomalies via hard logical decision splits.
* **Computational Superiority:** The proposed CPU-based TEG-XGBoost pipeline operates an order of magnitude faster during both training and inference compared to the hardware-accelerated 3D-CNN, making it highly suitable for rapid urban land-cover mapping.