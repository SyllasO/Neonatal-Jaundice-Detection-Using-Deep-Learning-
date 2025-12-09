# Neonatal Jaundice Detection Using Deep Learning

**ResNet50 • EfficientNetB0 • VGG16 • Custom CNN**  
*A medical imaging project with transfer learning, statistical testing, and Grad-CAM explainability*

[![Performance Summary](https://img.shields.io/badge/ResNet50-89.47%25-blue.svg)](https://github.com/SyllasO/Neonatal-Jaundice-Detection-Using-Deep-Learning-) [![EfficientNetB0](https://img.shields.io/badge/EfficientNetB0-86.18%25-green.svg)](https://github.com/SyllasO/Neonatal-Jaundice-Detection-Using-Deep-Learning-) [![Data Split](https://img.shields.io/badge/Split-70/15/15-orange.svg)](https://github.com/SyllasO/Neonatal-Jaundice-Detection-Using-Deep-Learning-)

> **Research prototype only. Not for clinical use or medical decision-making.**

---

## 📌 Project Overview

Neonatal jaundice affects **90% of newborns**, requiring early detection to prevent complications like kernicterus. This project evaluates **four CNN architectures** for **binary classification** (Jaundice vs Normal) from skin/sclera images:

- **ResNet50** (89.47% Test Accuracy - Best Performance)
- **EfficientNetB0** (86.18% - Best for Deployment)  
- **VGG16** (82.24% - Reference Baseline)
- **Custom CNN** (76.32% - From Scratch Baseline)

**Complete pipeline includes:**
- ✔️ **70/15/15 stratified train/val/test split**
- ✔️ Transfer learning with frozen ImageNet bases
- ✔️ Grad-CAM explainability visualizations
- ✔️ ROC/AUC analysis + McNemar's statistical test
- ✔️ Training/validation curves for all models

---

## 📂 Dataset

**Source:** [Kaggle Jaundice Image Dataset](https://www.kaggle.com/datasets/aiolapo/jaundice-image-data) by aiolapo

| Metric | Value |
|--------|-------|
| **Total Images** | 760 |
| **Normal** | 560 (73.7%) |
| **Jaundice** | 200 (26.3%) |
| **Resolution** | 224×224 |
| **Train/Val/Test** | **70/15/15** (stratified) |

jaundice-image-data/ # Direct from Kaggle
├── normal/ (560 images)
│ ├── Newborn 1.jpg
│ └── ...
└── jaundice/ (200 images)
├── Newborn 101.jpg
└── ...


---

## 🧪 Data Preprocessing

Kaggle Images (variable size) → Resize 224×224 → Normalize​
↓
Backbone-specific preprocessing + Train augmentation

| Model | Preprocessing |
|-------|---------------|
| **Custom CNN** | `rescale=1./255` |
| **ResNet50** | `resnet_preprocess` |
| **EfficientNetB0** | `efficientnet_preprocess` |
| **VGG16** | `vgg_preprocess` |

**Augmentations (Training only):**
- Rotation: ±15°
- Width/Height shift: 10%
- Horizontal flip

---

## 🏗️ Model Architectures & Results

| Model | Test Acc | Test F1 | ROC AUC | Size | Deployment |
|-------|----------|---------|---------|------|------------|
| **ResNet50** ⭐ | **89.47%** | **92.92%** | **0.957** | 84MB | Server |
| **EfficientNetB0** 🚀 | **86.18%** | **90.67%** | **0.935** | **16MB** | **Mobile** |
| **VGG16** | 82.24% | 88.11% | 0.910 | 528MB | Server |
| **Custom CNN** | 76.32% | 85.12% | 0.725 | ~22MB | Edge |

---

## 🧠 Grad-CAM Explainability (Test Set)

**High-confidence predictions from test set:**

- **ResNet50**: High-confidence **JAUNDICE** (P(Jaundice)=0.92) → Focuses on sclera/skin
- **EfficientNetB0**: High-confidence **NORMAL** (P(Normal)=0.95) → Focuses on healthy skin regions

**Clinical relevance:** Models attend to forehead, cheeks, sclera, and chest—standard jaundice assessment areas.

---

## 📈 Key Results

### **Test Set ROC Curves**
- Combined ROC curves for all four models on held-out test set
- AUC scores shown in legend vs random baseline (0.5)

### **Training Curves** 
- Train vs validation accuracy/loss for each model
- ResNet50 & EfficientNetB0 show smooth convergence with minimal overfitting

### **McNemar's Test** (ResNet50 vs EfficientNetB0)
Contingency Table (Test Set):
ResNet50
Correct Wrong
EffNet C: 121 10
W: 15 6

Chi-square = 0.640, p-value = 0.424 (p > 0.05)
**✅ No statistically significant difference** between top models.

---

## 🚀 Quick Start


---

## 🛠️ requirements.txt

tensorflow>=2.15.0
numpy
pandas
scikit-learn
matplotlib
pillow
statsmodels

---

## ⚠️ Medical Disclaimer

**Research/education only.** Requires:
- IRB approval
- Multi-center clinical validation  
- Regulatory clearance (FDA/CE)
- **Not for patient care**

---

## 📄 License & Citation

@misc{jaundice_detection_2025,
author = {SyllasO},
title = {Neonatal Jaundice Detection Using Deep Learning},
year = {2025},
publisher = {GitHub},
howpublished = {\url{https://github.com/SyllasO/Neonatal-Jaundice-Detection-Using-Deep-Learning}},
note = {Dataset: \url{https://www.kaggle.com/datasets/aiolapo/jaundice-image-data}}
}

---

## 🎯 Key Takeaways

1. **ResNet50** (89.47%) beats all models but **EfficientNetB0** (86.18%, 16MB) is production-ready
2. **Grad-CAM** shows clinically relevant attention (sclera/skin/forehead)
3. **McNemar's test** (p=0.424): Top models statistically equivalent
4. **70/15/15 split** ensures unbiased, reproducible test results



