# Changelog

All notable changes to this project will be documented in this file.

## [Unreleased]

## [1.0.0] - 2025-01-01
### Added
- End-to-end hyperspectral image classification pipeline using TEG + XGBoost
- Texture-Entropy-Gradient (TEG) feature descriptor implementation
  - Sobel operator for micro-edge (gradient) extraction
  - Local Entropy calculation for spatial disorder measurement
  - Multi-scale Local Binary Patterns (LBP) with configurable radius and n_points
- Dual execution modes:
  - `Light Mode` (18 features): pseudo-RGB composite + TEG for ultra-fast processing
  - `Heavy Mode` (618 features): full 103-channel spectral depth + TEG for maximum accuracy
- Impulse noise simulation (Salt-and-Pepper) across noise ratios from 0% to 20%
- Few-shot learning evaluation across training fractions: 1%, 5%, 10%, 20%, 50%, 70%
- PyTorch 3D-CNN baseline with support for CUDA, CPU, and Apple Silicon (MPS)
- Learning curve generation and performance comparison (TEG-XGBoost vs 3D-CNN)
- F1-Macro Score and Overall Accuracy (OA) evaluation metrics
- Computational profiling: feature extraction time, training time, inference time
- Visual classification maps: masked and full-scene prediction plots
- Pavia University hyperspectral dataset integration (PaviaU.mat / PaviaU_gt.mat)
- MNF (Minimum Noise Fraction) transformation utility for additional investigation
- Dataset visualization notebook (`visualize_dataset.ipynb`)
- `requirements.txt` with all dependencies
- MIT License
