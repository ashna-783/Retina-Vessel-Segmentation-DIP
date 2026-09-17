# Restoration and Segmentation of Retinal Blood Vessels Using CLAHE Enhancement and Morphological Thresholding

**Mini Project — Digital Image Processing (265DSEUBC302B)**
**Course Outcomes Addressed:** CO4 (Restoration & Enhancement), CO5 (Segmentation & Analysis)

## Problem Statement

Retinal fundus images are used by ophthalmologists to diagnose conditions such as
diabetic retinopathy, hypertension, and glaucoma. Manual tracing of blood vessels
in these images is time-consuming and error-prone. This project restores and
segments the blood vessel network from raw retinal fundus images using classical
digital image processing techniques (no deep learning).

## Dataset

- **DRIVE** (Digital Retinal Images for Vessel Extraction) dataset
- 15 images used (training split, image IDs 21–35), each 565×584 pixels
- Includes ground-truth vessel masks and field-of-view masks

## Methodology

```
Input Image → Green Channel Extraction → Restoration (Median Filter + CLAHE)
→ Segmentation (Black-hat Filtering + Otsu Thresholding) → Post-processing
→ Evaluation (Dice / IoU) → Result Comparison
```

An alternative segmentation method (adaptive thresholding) was also implemented
and compared against the primary Otsu-based approach.

## Results

| Method              | Avg. Dice | Avg. IoU |
|---------------------|-----------|----------|
| Black-hat + Otsu     | 0.583     | 0.413    |
| Adaptive Thresholding| 0.390     | 0.243    |

Otsu thresholding consistently outperformed adaptive thresholding across all 15
test images. See `report/` for the full analysis, including best-case and
worst-case discussion.

## Repository Structure

```
├── README.md
├── DIP_MINIPROJECT.ipynb     # Full source code (Google Colab notebook)
├── requirements.txt          # Python dependencies
├── images/                   # Sample input images from the dataset
├── screenshots/              # Result figures (comparison chart, best/worst case, etc.)
└── report/                   # Full project report (DOCX/PDF)
```

## How to Run

1. Install dependencies: `pip install -r requirements.txt`
2. Download the DRIVE dataset (e.g., from Kaggle:
   `andrewmvd/drive-digital-retinal-images-for-vessel-extraction`)
3. Open `DIP_MINIPROJECT.ipynb` in Jupyter or Google Colab
4. Update the dataset path if needed, and run all cells

## Limitations

- Small subset (15 images) used for the mini project
- Sensitive to illumination artifacts (glare/reflections)
- Thinnest peripheral vessels are often missed

## Future Scope

- Evaluate on the full DRIVE dataset and additional datasets (STARE, CHASE_DB1)
- Apply illumination correction before segmentation
- Compare against a deep-learning baseline (e.g., U-Net)
