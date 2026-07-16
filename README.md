# 👁️ Image Processing and Computer Vision — Course Assignments

This repository contains the complete solutions for the **Image Processing and Computer Vision** course assignments at the University of Bologna. The coursework spans two distinct paradigms of modern computer vision: **Classical Computer Vision** (mathematical and heuristic image processing) and **Deep Learning** (custom CNN architectures and transfer learning).

---

## 👥 Team Members

* **Şimal Yücel** — `simal.yucel@studio.unibo.it`
* **Davide Tonelli** — `davide.tonelli8@studio.unibo.it`
* **Giovanni Stea** — `giovanni.stea@studio.unibo.it`

---

## 📂 Repository Structure

    ├── assignment_module_one.ipynb   # Module 1: Classical CV (Coin Detection & Counting)
    ├── assignment_module_two.ipynb   # Module 2: Deep Learning (Aircraft Classification)
    ├── README.md                     # Project documentation
    └── data/                         # Datasets (downloaded automatically via notebooks)

---

## 🪙 Module 1: Coin Detection, Recognition and Counting

The first module focuses entirely on **classical, non-deep-learning computer vision techniques** implemented from scratch using Python and OpenCV. Given a reference image for each Euro denomination and 142 evaluation target photographs, the system detects every coin, identifies its denomination, and calculates the accurate monetary total per image.

### 🛠️ Pipeline Architecture
The detection and recognition pipeline is organized into four sequential stages:

    [ Input Photograph ]
             │
             ▼
     1. DETECTION        ──► Circle Hough Transform (dual channels) + Geometric/Photometric filters
             │
             ▼
     2. COLOR PROFILE    ──► CIELab statistics (Metal Hue, Chroma & Center-vs-Ring bimetal tests)
             │
             ▼
     3. APPEARANCE DESCR ──► Rotation-invariant polar correlation against reference templates
             │
             ▼
     4. SCALE CONSENSUS  ──► Per-image pixel-to-mm voting matrix for joint classification
             │
             ▼
    [ Final Count & Total ]

### ✨ Key Technical Highlights
* **Intelligent Color Space Analysis:** Evaluates candidate discs in the CIELab color space to achieve lightness-independent differentiation between copper (1c, 2c, 5c), gold (10c, 20c, 50c), and bimetallic (€1, €2) alloys.
* **Rotation-Invariant Template Matching:** Projects detected coin faces into a polar coordinate grid to compute normalized cross-correlations against reference coin engravings regardless of orientation.
* **Scale Consensus Voting:** Solves the varying camera distance problem without metadata. Every coin denomination hypothesis votes on a shared matrix for the correct resolution scale (mm/px) of the photograph. The highest-voted scale determines the final classification across all detected circles.
* **Relative vs. Absolute Metrics:** Demonstrates that within-coin contrasts (bimetal structures) and within-image ratios (scale consensus) survive illumination and distance shifts far better than rigid absolute thresholds.

---

## ✈️ Module 2: Fine-Grained Aircraft Classification

The second module explores **Deep Learning and Visual Recognition**, tackling fine-grained categorization on the challenging **FGVC-Aircraft** dataset (100 aircraft variants with subtle visual distinctions).

### 🔬 Part 1: Custom CNN from Scratch & Ablation Study
* **Architectural Design:** Built, trained, and optimized a custom Convolutional Neural Network (CNN) from scratch using PyTorch to learn specialized visual features for aircraft identification.
* **Rigorous Ablation Study:** Deconstructs the architecture by systematically removing or altering design components one at a time (such as specific layers, regularizers, or activation functions) to empirically quantify their individual contributions to validation accuracy and generalization.

### 🔄 Part 2: Transfer Learning & Fine-Tuning (ResNet-18)
* **Pretrained Adaptation:** Leverages a **ResNet-18** backbone pretrained on ImageNet-1K (V1) to perform transfer learning on the FGVC-Aircraft dataset.
* **Hyperparameter Regime Exploration:** * **Experiment 2A:** Evaluates fine-tuning performance when applying the exact training hyperparameters optimized for the scratch model in Part 1.
  * **Experiment 2B:** Adapts and optimizes hyperparameters specifically for the transfer learning regime (e.g., differential learning rates, warmup schedules, and modified weight decay), justifying each adjustment with empirical performance metrics.

---

## 💻 Setup and Installation

### Requirements
The projects require Python 3.8+ along with the following core libraries:
* PyTorch & Torchvision
* OpenCV (`opencv-python`)
* NumPy & Pandas
* Matplotlib & Seaborn
* Jupyter Notebook / Google Colab

### Installation & Execution
1. Clone the repository to your local machine:

    git clone https://github.com/your-username/your-repo-name.git
    cd your-repo-name

2. Install the required dependencies:

    pip install torch torchvision opencv-python numpy pandas matplotlib seaborn gdown

3. Launch Jupyter Notebook or open the files directly in Google Colab:

    jupyter notebook

*Note: Both notebooks contain self-contained data downloading scripts (using `gdown` or PyTorch datasets) that automatically retrieve and configure the necessary evaluation datasets upon execution.*

---

## 📜 License & Academic Integrity
This repository contains academic coursework developed for the Image Processing and Computer Vision curriculum at the University of Bologna. All rights reserved by the authors.
