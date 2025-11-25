## Robust Computer Vision point matching on lunar analog surface
### SIFT vs SuperPoint vs SuperPoint+SuperGlue on the POLAR Dataset

In this project I evaluate 3 different methods for interest point detection and matching on lunar-like terrain images: **SIFT**, a classical computer vision algorithm, and **SuperPoint**, a modern deep-learning-based feature extractor and **Superpoin+SuperGlue**. 

**What is the problem?**  
Feature matching on lunar imagery is challenging due to extreme illumination variations (deep shadows, backlighting, high contrast). These conditions significantly affect the stability of keypoints and descriptors.

**Why is it important?**  
Robust feature matching is a fundamental step in the reconstruction of Digital Elevation Models (DEMs), visual navigation, and terrain mapping for lunar exploration missions.

**What methods are we comparing?**  
- **SIFT** for classical, geometry-driven features  
- **SuperPoint** for learned feature extraction  
- **SuperGlue** for learned correspondence refinement

**What is the goal of the work?**  
To evaluate and compare the robustness of these methods under illumination and viewpoint changes, using sample data from the **NASA POLAR Traverses** dataset, which simulates lunar polar lighting conditions.


## What was done

The project follows a three-step workflow:  
**(1) keypoint detection**, **(2) feature matching**, and **(3) robustness evaluation through heatmaps**.

### 1. Keypoint Detection

The first step of the pipeline consists in identifying **distinctive and repeatable interest points** in the input POLAR images.  
These are points that should remain detectable despite changes in illumination or viewpoint, making them suitable for matching.

- With **SIFT**, keypoints are detected using a scale-space search (Difference of Gaussians), followed by orientation assignment to ensure invariance to rotation and scale.  
  This produces sparse but geometrically stable features on lunar-like scenes:  
  ![SIFT Keypoints](img/SIFT_points.png)

- With **SuperPoint**, keypoints are detected by a deep neural network trained to identify repeatable interest points even under strong photometric variation.  
  This results in denser keypoints and a different spatial distribution, reflecting the learned nature of the detector:  
  ![SuperPoint Keypoints](img/SuperPoint_points.png)

Together, these visualizations show how classical and learned detectors behave when exposed to harsh illumination conditions typical of lunar terrains.


---

### 2. Feature Matching

After detecting keypoints, the next step is to establish **correspondences** between two images captured under different exposure or viewpoint settings.  
Matching is essential for geometric verification, pose estimation, stereo reconstruction, and DEM generation.

- With **SIFT**, matching is performed using descriptor comparison (typically nearest-neighbor search) followed by ratio filtering to remove ambiguous matches.  
  This step provides a classical baseline for geometric consistency under illumination variation.  
  ![SIFT Matching](img/SIFT_matching.png)

- With **SuperPoint**, descriptors are matched using nearest-neighbor search in the learned descriptor space.  
  This allows us to evaluate how learned features behave under strong photometric differences.  
  ![SuperPoint Matching](img/SuperPoint_matching.png)

- With **SuperPoint + SuperGlue**, correspondences are refined using a graph neural network that performs attention-based message passing between keypoints.  
  The matcher incorporates spatial context and produces more stable and coherent correspondences.  
  ![SuperGlue Matching](img/SuperGlue_matching.png)

These matching outputs represent the core of the evaluation: how reliably each pipeline can connect the same physical points across challenging lunar-analog images.


---

### 3. Robustness Evaluation (Heatmaps)
Finally, I evaluated how stable the matches were across all exposure combinations.  
For each pair, I computed **RANSAC inlier ratios**, then organized them into heatmaps.

Below are the heatmaps produced for all methods under both scenarios:  
**same viewpoint** (illumination change only) and **different viewpoint** (illumination + geometry change).

## Heatmap Comparison

A direct visual comparison of the robustness of all three methods under the two experimental scenarios:

| **Method**                 | **Same Viewpoint, Different Illumination** | **Different Viewpoint, Different Illumination** |
|---------------------------|---------------------------------------------|------------------------------------------------|
| **SIFT**                  | ![SIFT Same](img/SIFT.png)                  | ![SIFT Diff](img/SIFT_diff.png)                |
| **SuperPoint**            | ![SP Same](img/SuperPoint.png)              | ![SP Diff](img/SuperPoint_diff.png)            |
| **SuperPoint + SuperGlue**| ![SG Same](img/SuperGlue.png)               | ![SG Diff](img/SuperGlue_diff.png)             |


These heatmaps represent the final stage of the pipeline, summarizing the overall robustness of each method under varying exposure and viewpoint conditions.

---

## Key Takeaways

- **SIFT** remains more robust to viewpoint differences but suffers under extreme illumination changes.  
- **SuperPoint** is highly resilient to exposure changes but loses consistency when geometry varies.  
- **SuperPoint + SuperGlue** improves match stability, especially under illumination variation, but still struggles with wide-baseline geometry.  
- No single method dominates in all conditions, making the choice method-dependent: illumination-driven tasks favor learned features, while geometric changes favor classical approaches.
