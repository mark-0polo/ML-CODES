# A Large-Scale, Fine-Grained Image Dataset for Industrial Hardware Component and Tool Recognition

[![Dataset DOI](https://img.shields.io/badge/DOI-10.17632%2Fgmjkzdxhc6.1-blue.svg)](https://doi.org/10.17632/gmjkzdxhc6.1)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Python](https://img.shields.io/badge/Python-3.10%2B-brightgreen.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.2.1-orange.svg)](https://pytorch.org/)

Official code repository for the technical validation pipelines accompanying the *Scientific Data* (Nature Portfolio) manuscript:  
**"A Large-Scale, Fine-Grained Image Dataset for Industrial Hardware Component and Tool Recognition"**

---

## 📌 Dataset Access & DOI
The complete dataset is publicly released and hosted on **Mendeley Data**:
* **DOI:** [10.17632/gmjkzdxhc6.1](https://doi.org/10.17632/gmjkzdxhc6.1)
* **Direct Link:** [https://doi.org/10.17632/gmjkzdxhc6.1](https://doi.org/10.17632/gmjkzdxhc6.1)
* **License:** Creative Commons Attribution 4.0 International (CC BY 4.0)
* **Contents:**
  - `raw/`: 4,510 unaugmented workshop images collected across three distinct smartphone camera modules (OnePlus Nord CE 4, Nothing CMF Phone 2 Pro, and Nothing Phone 2) with COCO-format bounding box annotations.
  - `augmented/`: 12,115 benchmark images (10,133 train, 993 validation, 989 test; 13,271 annotated instances) in COCO JSON formats across 24 fine-grained tool categories.

---

## 📂 Repository Notebooks & Validation Roles

| Notebook File | Model Architecture | Validation Role |
| :--- | :--- | :--- |
| `YOLO_V_8s.ipynb` | Ultralytics YOLOv8s | Supervised detection baseline (Convolutional) |
| `YOLO_V_11s.ipynb` | Ultralytics YOLO11s | Supervised detection baseline (Convolutional) |
| `YOLO_V_12s.ipynb` | Ultralytics YOLOv12s | Supplementary supervised detection evaluation |
| `YOLO_V_26s.ipynb` | Ultralytics YOLO26s | Modern supervised detection baseline |
| `RFDETR.ipynb` | RF-DETR-Small | Supervised transformer detection baseline |
| `DINOv2_Feature_Clustering.ipynb` | **DINOv2 (ViT-S/14 & ViT-B/14)** | Self-supervised foundation feature extraction, PCA, KMeans, GMM, and Hungarian assignment |

---

## ⚙️ Software Stack & Environment Setup

All experiments were executed on **Google Colab Pro (NVIDIA T4 GPU)** using **Python 3.10.12**.

To install the dependencies used across all validation scripts, run:

```bash
pip install torch==2.2.1 torchvision==0.17.1 --index-url https://download.pytorch.org/whl/cu121
pip install ultralytics==8.3.0
pip install rfdetr==0.0.1
pip install supervision==0.23.0
pip install scikit-learn==1.4.1 scipy==1.13.0
pip install matplotlib==3.8.3 seaborn==0.13.2 umap-learn==0.5.6
pip install roboflow==1.1.27
```

---

## 🚀 How to Run the Technical Validation

### 1. Supervised Object Detection (YOLO Variants & RF-DETR)
1. Download and extract the dataset from Mendeley Data (`10.17632/gmjkzdxhc6.1`).
2. Open the desired notebook (e.g., `YOLO_V_11s.ipynb` or `RFDETR.ipynb`) in Google Colab or Jupyter Notebook.
3. Update the dataset directory path in the notebook to point to your unzipped dataset location.
4. Run all cells to train for 50 epochs and compute precision, recall, mAP@0.5, mAP@0.5:0.95, and confusion matrices.

### 2. Self-Supervised Feature Clustering (DINOv2)
1. Open `DINOv2_Feature_Clustering.ipynb` in Google Colab.
2. The notebook automatically downloads Meta's official pretrained DINOv2 foundation models (`dinov2_vits14` and `dinov2_vitb14`) via PyTorch Hub.
3. Object crops resized to 518×518 pixels are mapped into high-dimensional feature space.
4. Dimensionality reduction via PCA (100 components) is executed, followed by clustering ($K = 24$) with KMeans, MiniBatchKMeans, and Gaussian Mixture Models (GMM).
5. Hungarian matching aligns unsupervised clusters with class labels to compute purity metrics (Adjusted Rand Index, Normalized Mutual Information, Silhouette score, and Davies–Bouldin index).

---

## 📜 Citation

If you use this dataset or code in your research, please cite our corresponding publications:

```bibtex
@article{mondol2026hardware,
  title={A Large-Scale, Fine-Grained Image Dataset for Industrial Hardware Component and Tool Recognition},
  author={Mondol, Mark Protik and Islam, Md Shakib Al and Alsaawy, Yazed B. and Hossain, Tanvir and Rabbi, Abu Sayed and Islam, Md Motaharul},
  journal={Scientific Data},
  year={2026}
}

@misc{dataset2026mendeley,
  title={Hardware Tools Complete Dataset},
  author={Mondol, Mark and Islam, Md Shakib Al and Hossain, Tanvir and Rabbi, Abu Sayed and Islam, Md Motaharul},
  year={2026},
  publisher={Mendeley Data},
  version={V1},
  doi={10.17632/gmjkzdxhc6.1}
}
```

---

## 📄 License
* Code scripts and notebooks in this repository are available under the **MIT License**.
* The hardware image dataset is shared under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.
