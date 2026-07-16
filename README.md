# Coin-Detection-with-CV-

# 🪙 Coin Detection, Recognition and Counting

This project implements a classical, non-deep-learning computer vision pipeline in Python using OpenCV to detect, recognize, and count Euro coins from digital photographs[cite: 2]. Given reference images for each denomination, the system identifies every coin in a target image, determines its denomination, and computes the monetary total[cite: 2].

---

## 🚀 Key Features

* **Classical CV Approach:** Relies entirely on traditional image processing and geometric heuristics instead of deep learning[cite: 2].
* **Intelligent Color Analysis:** Uses CIELab statistics to accurately differentiate between copper, gold, and bimetallic (€1 and €2) coins[cite: 2].
* **Rotation-Invariant Matching:** Uses polar-warped correlation alignment to match coin faces regardless of their orientation[cite: 2].
* **Scale Consensus Voting:** Dynamically estimates the physical scale (mm-per-pixel) of each photograph based on collective voting from all candidate coins[cite: 2].
* **Precise Accounting:** Handles financial values safely using integer cents internally[cite: 2].

---

## 🛠️ Pipeline Architecture

The processing pipeline is organized into four main stages[cite: 2]:


[ Input Image ]
│
▼

1. DETECTION        ──► Hough Transform on dual channels + Geometric/Photometric filters
│
▼
2. COLOR PROFILE    ──► CIELab statistics (Metal Hue, Chroma & Ring-vs-Center tests)
│
▼
3. APPEARANCE DESCR ──► Rotation-invariant polar correlation vs Reference coins
│
▼
4. SCALE CONSENSUS  ──► Per-image pixel-to-mm voting matrix for joint classification
│
▼
[ Final Count & Total ]


1. **Detection:** Candidate coin locations are proposed using the Circle Hough Transform executed across multiple optimal image channels, followed by geometric and photometric plausibility filters[cite: 2].
2. **Color Description:** Extracts statistical profiles in the CIELab color space to divide coins into their respective alloy families (Copper, Gold, or Bimetallic). A dedicated inner-disc vs. outer-ring check isolates €1 and €2 variants[cite: 2].
3. **Appearance Description:** Projects the localized coins into a polar coordinate grid to calculate rotation-invariant cross-correlations against high-resolution reference templates[cite: 2].
4. **Joint Classification (Scale Consensus):** Solves the varying camera distance problem. Every coin denomination hypothesis votes on a shared matrix for the correct resolution scale ($mm/px$) of the image[cite: 2]. The highest-voted scale dictates final labels[cite: 2].

---

## 📊 Supported Denominations

The system evaluates the complete Euro coin lifecycle with official dimensions[cite: 2]:

| Denomination | Value (Cents) | Alloy Family | Diameter (mm) |
| :--- | :---: | :--- | :--- |
| **1 Cent** | 1 | Copper | 16.25 mm |
| **2 Cent** | 2 | Copper | 18.75 mm |
| **5 Cent** | 5 | Copper | 21.25 mm |
| **10 Cent** | 10 | Gold | 19.75 mm |
| **20 Cent** | 20 | Gold | 22.25 mm |
| **50 Cent** | 50 | Gold | 24.25 mm |
| **1 Euro** | 100 | Bimetal | 23.25 mm |
| **2 Euro** | 200 | Bimetal | 25.75 mm |

---

## 💻 Prerequisites & Setup

### Requirements
* Python 3.8+
* OpenCV (`opencv-python`)
* NumPy
* Pandas
* Matplotlib

### Installation
1. Clone the repository:
   ```bash
   git clone [https://github.com/simalyucel/Coin-Detection-and-Counting.git](https://github.com/simalyucel/Coin-Detection-and-Counting.git)
   cd Coin-Detection-and-Counting



2. Install dependencies:
```bash
pip install numpy opencv-python pandas matplotlib gdown

```



---

## 📂 Dataset Structure

The project expects a data directory named `coin_dataset/` structured as follows:


coin_dataset/
├── reference_set/
│   ├── 1cent.jpg
│   ├── 2cent.jpg
│   └── ... (up to 2euro.jpg)
└── target_set/
    ├── image_1.jpg
    ├── image_2.jpg
    └── ... (142 target evaluation photographs)



Note: If running inside Google Colab, the notebook includes an integrated downloader that securely fetches and extracts the dataset structure automatically via `gdown`.

---

## ⚠️ Important Implementation Notes

### Color Space Awareness

Standard loaders like `cv2.imread()` extract pixels in **BGR** format. While the reference set behaves normally upon swapping to **RGB**, the target JPEG dataset contains native pre-reversed matrix configurations. The codebase deploys isolated target loading adapters to prevent shifting copper into cyan profiles, protecting downstream color filters.

```text
Reference 50c center check (Imread order): [  46.7   69.2  105.4 ] -> Red Dominates (True BGR)
Target image_81 center check (Imread order): [ 184.4  167.1   98.3 ] -> Blue Dominates (Pre-reversed)

```

---

## 📜 License

This project is developed for academic evaluation purposes under the Artificial Intelligence degree modules. All rights reserved.

```

```
