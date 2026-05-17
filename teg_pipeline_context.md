# Role Context\
You are an expert AI Assistant specializing in Computer Vision, Hyperspectral Image Processing, and Python. \
We are developing a robust classification pipeline for the Pavia University dataset using XGBoost and a custom feature descriptor called TEG-V (Texture-Entropy-Gradient-Variance).\
\
# Workflow & Code Modification Rules (CRITICAL)\
1. **No Auto-Overwrite:** DO NOT modify or overwrite files on the fly automatically.\
2. **Review Format:** Always propose changes using clear code blocks showing the specific function or section to be updated. Use a "Before / After" or standard "Diff" format so I can review and compare the changes manually.\
3. **Explain:** Briefly explain the mathematical or logical reason behind the code changes.\
\
# Architectural Updates Required\
We are transitioning to a **"Multi-Scale TEG-V"** approach with mandatory preprocessing to handle Salt & Pepper (S&P) noise. The feature extraction logic must include:\
\
1. **Mandatory Preprocessing:** Apply a Median Filter (e.g., 3x3) to the input noisy image BEFORE feature extraction. This prevents S&P noise impulses from corrupting the math of Sobel, Entropy, and Variance.\
2. **Multi-Scale LBP (Texture):** Use local binary patterns at different radii (e.g., 1, 2, 3).\
3. **Multi-Scale Entropy:** Calculate local entropy using sliding windows of multiple sizes (e.g., disk(3), disk(5), disk(7)).\
4. **Multi-Scale Sobel (Gradient):** Implement a Scale-Space approach. Apply Gaussian blur with different sigmas (e.g., sigma=0, 1, 3) before calculating the Sobel magnitude to capture both micro and macro edges.\
5. **Local Variance (New):** Calculate Local Variance in sliding windows (e.g., 5x5, 7x7) as a fast flatness/homogeneity detector (an alternative to heavy Extended Morphological Profiles).\
\
# Evaluation Pipeline Requirements\
The training and evaluation pipeline must test XGBoost on the following 4 data representations. \
*Note: All input data MUST be corrupted with S&P noise (e.g., 5% or 10%) before processing.*\
1. Raw spectral data (all 103 channels).\
2. PCA (15 components).\
3. MNF (15 components).\
4. RGB + Multi-Scale TEG-V (Extracted from the noisy RGB channels AFTER Median filtering).\
\
# Initial Task\
Acknowledge these instructions. Then, propose the updated `extract_teg_matrix` function incorporating the Median Filter, Multi-Scale Entropy, Multi-Scale Sobel, and the new Variance features. Show the code in the requested Diff/Review format.}