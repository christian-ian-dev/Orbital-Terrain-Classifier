# Orbital Terrain Classifier: Robust CNN for Satellite Imagery 

---

<br> 

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/) [![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)](https://pytorch.org/) 

---

<br> 

 ## Project Overview 

---

<br>

This project implements a Convolutional Neural Network (CNN) built in PyTorch to autonomously classify terrestrial features using the EuroSAT Sentinel-2 dataset. 

<br>

---

Designed with aerospace deployment in mind, this project goes beyond standard classification by stress-testing the model against simulated sensor degradation (radiation noise) and utilizing Explainable AI (Grad-CAM) to audit the model's decision-making process.

<br>

---

<br>

**Key Features:** 

---

<br>

* **Leakage-Free Pipeline:** Strict isolation of Train/Validation/Test splits (70/15/15) with dynamic data augmentation (rotations, flips) applied exclusively to the training set. * **Environmental Robustness Testing:**Evaluation of model performance under injected Gaussian noise to simulate single-event upsets (SEUs) and sensor degradation in orbital environments. * **Explainable AI (XAI):** Implementation of Grad-CAM to eliminate the "black box" effect, ensuring the network classifies terrain based on valid topographical structures rather than spurious background artifacts. 

<br>

---

<br>

##  Technology Stack 

---

<br>

* **Frameworks:** PyTorch, Torchvision * **Languages:** Python ***Data Processing:** NumPy, OpenCV * **Visualization:** Matplotlib * **Hardware:** NVIDIA T4 Tensor Core GPU (via Google Colab)

<br>

---

<br>

## Performance & Robustness Metrics 

---

<br>

### Baseline Performance (Clean Data) The model was trained over 15 epochs. It successfully converged without overfitting, achieving a final holdout test accuracy of **95.2%**. 

<br>

---

<br>

![Training Curve](https://github.com/christian-ian-dev/Orbital-Terrain-Classifier/blob/b1bcc4e5f69fd7839c956c798a86bdbc06d15396/images/learning_curve.png)

<br>

---

<br>

 ### Simulating Orbital Sensor Noise To simulate the harsh realities of space deployment (e.g., atmospheric interference, radiation-induced sensor noise), Gaussian noise $N(0, \sigma^2)$ was mathematically injected into the test data. 

<br>

---

<br>

***Clean Baseline:** 95.2% Accuracy * **Low Noise Injection ($\sigma=0.3$):** 88.7% Accuracy * **High Noise Injection ($\sigma=0.7$):** 71.4% Accuracy 

<br>

---

<br>

![Noise Degradation Chart](https://github.com/christian-ian-dev/Orbital-Terrain-Classifier/blob/b1bcc4e5f69fd7839c956c798a86bdbc06d15396/images/noise_degradation.png)

<br>

---

<br>
 
**Analysis:** 

---

<br>

While standard CNNs perform well on pristine data, the 23.8% drop in accuracy under high noise highlights the necessity of radiation-hardened hardware and noise-aware training methodologies for deep-space missions.

<br>

---

<br>

##  Model Transparency (Grad-CAM)

---

<br>

 In mission-critical environments, accuracy without transparency is a liability. Grad-CAM was implemented to trace the gradients of the final convolutional layer (`conv2`), producing heatmaps that highlight the exact pixels driving the AI's classification. 

<br>

---

<br>

![Grad-CAM Heatmap](https://github.com/christian-ian-dev/Orbital-Terrain-Classifier/blob/b1bcc4e5f69fd7839c956c798a86bdbc06d15396/images/gradcam_output.png)

<br>

---

<br>

 > **Figure 1:** The model correctly identifying a `River` class. The spatial heatmap demonstrates the AI is actively tracking the curvature of the waterbed rather than memorizing surrounding forest textures, proving topographical feature extraction.

<br>

---

<br>

##  How to Run Locally 1. 

---

<br>

**Clone the repository:** 

<br>

---

<br>

```bash 
git clone [https://github.com/](https://github.com/)[YourUsername]/Orbital-Terrain-Classifier.git cd Orbital-Terrain-Classifier