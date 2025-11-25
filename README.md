# Robust Interest Point Matching on Lunar-Analog Imagery  
### SIFT vs SuperPoint vs SuperGlue on the NASA POLAR Dataset

This project benchmarks three feature-matching pipelines under challenging illumination and viewpoint variations using lunar-analog images from the **NASA POLAR Traverses** dataset:

- **SIFT** — classical keypoints and descriptors  
- **SuperPoint** — deep-learning feature extractor  
- **SuperPoint + SuperGlue** — learned keypoints + GNN-based matcher  

The goal is to evaluate how robust these methods are to conditions typical of lunar polar environments, where extreme exposure differences and geometric variations make feature matching difficult.  
This is relevant for tasks such as Digital Elevation Model (DEM) reconstruction, rover navigation, and visual localization.

---

## Dataset
The experiments use a subset of the **NASA POLAR Traverses** dataset, which replicates lunar-like illumination conditions such as deep shadows, harsh contrasts, and backlighting.  
In this project, images from traverse location `loc00m` were used, with controlled variation in **exposure** and **viewpoint**.

---

## Experimental Scenarios

Two controlled scenarios were tested:

1. **Same Viewpoint, Different Exposure**  
   Tests photometric robustness without geometric variation.

2. **Different Viewpoint, Different Exposure**  
   Combines illumination changes with geometric shifts, representing a more realistic and challenging setting.

Each image pair is evaluated using **RANSAC inlier ratio** to quantify the correctness of feature correspondences.

---

## Key Findings

- **SIFT**  
  More robust to viewpoint changes but sensitive to strong illumination variation.

- **SuperPoint**  
  Very robust to illumination changes when viewpoint is fixed, but performance drops under geometric variation.

- **SuperPoint + SuperGlue**  
  Improves SuperPoint consistency under difficult lighting, but wide-baseline geometry remains challenging.

Overall, no method dominates in all conditions. Classical and learned features show complementary strengths depending on whether **illumination** or **geometry** is the dominant source of difficulty.

---

## Future Improvements

- Extend the experiments to a larger subset of the POLAR dataset.  
- Add more matching methods (ORB, R2D2, D2-Net, ALIKED).  
- Include additional quantitative metrics (repeatability, precision/recall, pose error).
