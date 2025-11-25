### SIFT vs SuperPoint vs SuperPoint+SuperGlue on the POLAR Dataset

In this notebook I evaluate 3 different methods for interest point detection and matching on lunar-like terrain images: **SIFT**, a classical computer vision algorithm, and **SuperPoint**, a modern deep-learning-based feature extractor and **Superpoin+SuperGlue**. 

**What is the problem?**  
Feature matching on lunar imagery is challenging due to extreme illumination variations (deep shadows, backlighting, high contrast). These conditions significantly affect the stability of keypoints and descriptors.

**Why is it important?**  
Robust feature matching is a fundamental step in the reconstruction of **Digital Elevation Models (DEMs)**, visual navigation, and terrain mapping for lunar exploration missions.

**What methods are we comparing?**  
- **SIFT** for classical, geometry-driven features  
- **SuperPoint** for learned feature extraction  
- **SuperGlue** for learned correspondence refinement

**What is the goal of the work?**  
To evaluate and compare the robustness of these methods under illumination and viewpoint changes, using sample data from the **NASA POLAR Traverses** dataset, which simulates lunar polar lighting conditions.
