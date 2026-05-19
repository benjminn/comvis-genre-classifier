# 🎬 Movie Poster Multi-Label Genre Classification

This project compares three modern deep learning architectures — **ResNet-50**, **CLIP ViT-L/14**, and **SigLIP** — for multi-label genre classification of movies based on their poster images. All three models are trained and evaluated using an **identical, standardized pipeline** to ensure a scientifically valid apples-to-apples comparison.

> 📄 **Associated Paper:** *"Multi-Label Movie Poster Genre Classification: A Comparative Study of ResNet-50, CLIP, and SigLIP"* — Lisa Olivia Putri Maharani, Benjamin Sigit, Rafeyfa Asyla. DTETI, Universitas Gadjah Mada, 2025.

---

## 👥 Authors

| Name | NIM | Institution |
|---|---|---|
| Lisa Olivia Putri Maharani | 23/519241/TK/57250 | Teknologi Informasi, DTETI — Universitas Gadjah Mada |
| Benjamin Sigit | 23/514737/TK/56513 | Teknologi Informasi, DTETI — Universitas Gadjah Mada |
| Rafeyfa Asyla | 23/512856/TK/56361 | Teknologi Informasi, DTETI — Universitas Gadjah Mada |

---

## 📁 File Structure

```
project-akhir/
│
├── 1. project pytorch Resnet50 kvold.ipynb   # ResNet50 K-Fold Notebook
├── 2. project pytorch CLIP kfold.ipynb       # CLIP ViT-L/14 K-Fold Notebook
├── 3. project pytorch siglip-updated.ipynb   # SigLIP K-Fold Notebook
│
├── 1. Output resnet/                         # ResNet50 model outputs
│   ├── resnet50_multilabel_poster_model.pt   # ⚠️ Not included — (inside drive)
│   ├── submission.csv
│   ├── test_predictions.csv
│   ├── thresholds.json
│   ├── cv_fold_metrics_default.csv
│   ├── cv_fold_metrics_tuned.csv
│   ├── genre_distribution.png
│   ├── per_genre_performance.png
│   ├── prediction_heatmap.png
│   ├── sample_predictions.png
│   └── training_history.png
│
├── 2. Output CLIP/                           # CLIP model outputs
│   ├── clip_multilabel_poster_model.pt       # ⚠️ Not included — (inside drive)
│   ├── submission.csv
│   ├── test_predictions.csv
│   ├── thresholds.json
│   ├── cv_fold_metrics_default.csv
│   ├── cv_fold_metrics_tuned.csv
│   ├── genre_distribution.png
│   ├── genre_cooccurrence.png
│   ├── class_imbalance.png
│   ├── per_genre_performance.png
│   ├── prediction_heatmap.png
│   ├── sample_posters.png
│   ├── sample_predictions.png
│   └── training_history.png
│
├── 3. Output siglip/                         # SigLIP model outputs
│   ├── siglip_multilabel_poster_model.pt     # ⚠️ Not included — (inside drive)
│   ├── submission.csv
│   ├── test_predictions.csv
│   ├── thresholds.json
│   ├── cv_fold_metrics_default.csv
│   ├── cv_fold_metrics_tuned.csv
│   ├── genre_distribution.png
│   ├── per_genre_performance.png
│   ├── prediction_heatmap.png
│   ├── sample_predictions.png
│   └── training_history.png
│
└── Datasets/
    ├── images/
    │   ├── train/   # 250 poster images (1.jpg – 250.jpg)
    │   └── test/    # 50 poster images (251.jpg – 300.jpg)
    └── genre.xlsx   # Multi-label annotations (14 genres)
```

---

## 📥 Pre-trained Model Downloads

Model checkpoint files (`.pt`) exceed GitHub's file size limit and are hosted on Google Drive.

| Model | Size | Download Link |
|---|---|---|
| ResNet50 | ~98 MB | [Download ResNet50 Checkpoint](https://drive.google.com/drive/folders/1sNylQ5J3JY-UUvjLDLIHXaWqVKLlsMMM?usp=sharing) |
| CLIP ViT-L/14 | ~1.2 GB | [Download CLIP Checkpoint](https://drive.google.com/drive/folders/1sNylQ5J3JY-UUvjLDLIHXaWqVKLlsMMM?usp=sharing) |
| SigLIP | ~373 MB | [Download SigLIP Checkpoint](https://drive.google.com/drive/folders/1sNylQ5J3JY-UUvjLDLIHXaWqVKLlsMMM?usp=sharingP) |

---

## 📦 Requirements

### Python Version
```
Python >= 3.10
```

### Installation

```bash
pip install torch torchvision open-clip-torch transformers \
            iterative-stratification scikit-learn pandas openpyxl \
            numpy matplotlib seaborn tqdm pillow
```

| Model | Additional Library |
|---|---|
| ResNet50 | `torchvision` (included with PyTorch) |
| CLIP ViT-L/14 | `open-clip-torch` |
| SigLIP | `transformers >= 4.35.0` |

---

## 🗄️ Dataset

> 🔗 **Dataset Download:** The full dataset is available on Kaggle: [Computer Vision Poster Dataset](https://www.kaggle.com/datasets/benjaminsigit/computer-vision-poster-dataset)

| | Details |
|---|---|
| **Total images** | 300 JPEG movie posters sourced from IMDb |
| **Training set** | 250 images (`1.jpg` – `250.jpg`) |
| **Test set** | 50 images (`251.jpg` – `300.jpg`) |
| **Labels per poster** | 1–8 genres simultaneously active (mean ≈ 3.9) |
| **Label format** | Binary multi-label (0/1) per genre |
| **Label file** | `genre.xlsx` with `filename` + 14 genre columns |

### 14 Classified Genres
```
action | adventure | animation | comedy | crime  | drama
family | fantasy   | horror    | musical | mystery | romance
scifi  | thriller
```

### Training Data Distribution

| Genre | Train (+) | Train (%) | Test (+) | Imbalance Ratio |
|---|---|---|---|---|
| action | 167 | 66.8% | 36 | 0.50x |
| drama | 146 | 58.4% | 34 | 0.71x |
| adventure | 125 | 50.0% | 22 | 1.00x |
| comedy | 80 | 32.0% | 13 | 2.13x |
| thriller | 75 | 30.0% | 21 | 2.33x |
| scifi | 72 | 28.8% | 14 | 2.47x |
| fantasy | 71 | 28.4% | 11 | 2.52x |
| crime | 48 | 19.2% | 13 | 4.21x |
| animation | 47 | 18.8% | 8 | 4.32x |
| mystery | 41 | 16.4% | 13 | 5.10x |
| romance | 38 | 15.2% | 1 | 5.58x |
| family | 35 | 14.0% | 4 | 6.14x |
| horror | 22 | 8.8% | 3 | 10.36x |
| **musical** | **5** | **2.0%** | **0** | **49.00x** (most imbalanced) |

> **Imbalance Ratio** = negatives / positives per genre. Musical (49:1) is handled via `pos_weight` in the loss function.

---

## 🏗️ Model Architecture

### Shared Classification Head (Identical Across All Models)

```
LayerNorm(feature_dim)
    ↓
Dropout(0.3)
    ↓
Linear(feature_dim → 512)
    ↓
GELU()
    ↓
Dropout(0.2)
    ↓
Linear(512 → 14)    ← raw logits
    ↓
Sigmoid()           ← per-genre probability
```

The only difference between models in this head is `feature_dim`: **2048** for ResNet-50, **768** for CLIP and SigLIP.

---

### 1. 🔷 ResNet-50 (Classical CNN Baseline)

| Component | Details |
|---|---|
| **Base model** | `torchvision.models.resnet50(IMAGENET1K_V2)` |
| **Pretraining corpus** | ImageNet-1K |
| **Encoder parameters** | 23.5M |
| **Feature dimension** | 2048 |
| **Frozen layers** | `layer1`, `layer2`, `layer3` |
| **Fine-tuned layers** | `layer4` (last residual block) + head |
| **Normalization** | ImageNet: mean=(0.485, 0.456, 0.406), std=(0.229, 0.224, 0.225) |
| **Checkpoint size** | ~98 MB |

**Advantages:**
- ✅ Lightweight and fast to train (~8s per epoch)
- ✅ No special libraries required
- ✅ No internet dependency during training

**Disadvantages:**
- ❌ Pretrained only on ImageNet object classification — limited visual diversity for poster-genre cues
- ❌ CNN architecture integrates information locally, missing global compositional cues
- ❌ Substantially lower performance than Vision-Language Models (~15 Macro-F1 pts gap)

---

### 2. 🔶 CLIP ViT-L/14 (Vision-Language Model)

| Component | Details |
|---|---|
| **Base model** | `open_clip: ViT-L-14 (openai pretrained)` |
| **Pretraining corpus** | WIT-400M (400M image-text pairs) |
| **Encoder parameters** | 303.5M |
| **Feature dimension** | 768 |
| **Pretraining objective** | Symmetric softmax contrastive loss |
| **Frozen layers** | All except last transformer block |
| **Fine-tuned layers** | `visual.transformer.resblocks[-1]` + head |
| **Normalization** | CLIP: mean=(0.4815, 0.4578, 0.4082), std=(0.2686, 0.2613, 0.2758) |
| **Checkpoint size** | ~1.2 GB |

**Advantages:**
- ✅ Trained on 400M image-text pairs — rich semantic representations
- ✅ Captures typographic, compositional, and stylistic poster cues
- ✅ Strongest single-genre results on drama (F1=0.96), mystery (F1=0.63), comedy (F1=0.86)

**Disadvantages:**
- ❌ Largest checkpoint (~1.2 GB), slowest training (~480s per epoch)
- ❌ Softmax contrastive pretraining is less structurally aligned with multi-label inference than SigLIP
- ❌ Requires `open-clip-torch`

---

### 3. 🟢 SigLIP (Sigmoid Loss Vision-Language Model)

| Component | Details |
|---|---|
| **Base model** | `google/siglip-base-patch16-224` (HuggingFace) |
| **Pretraining corpus** | WebLI (web-scale image-language) |
| **Encoder parameters** | 86.2M |
| **Feature dimension** | 768 |
| **Pretraining objective** | Pairwise sigmoid loss (each image-text pair scored independently) |
| **Frozen layers** | All except last encoder layer |
| **Fine-tuned layers** | `siglip.encoder.layers[-1]` + head |
| **Preprocessing** | `SiglipImageProcessor` (bilinear resize + normalize) |
| **Checkpoint size** | ~373 MB |

**Advantages:**
- ✅ Sigmoid pretraining mirrors per-genre binary inference — structural alignment with multi-label tasks
- ✅ Best overall test performance: Micro-F1=0.839, Macro-F1=0.688
- ✅ Compact (86M params) yet competitive with CLIP's 303M params
- ✅ Perfect F1=1.00 on animation and horror

**Disadvantages:**
- ❌ Sensitive to augmentation outside its pretraining distribution
- ❌ `SiglipImageProcessor` does not support custom torchvision augmentations natively
- ❌ Requires HuggingFace `transformers`

---

## ⚙️ Training Configuration

All hyperparameters are **identical across all three models**. Key differences are noted in the rightmost columns.

| Setting | ResNet-50 | CLIP ViT-L/14 | SigLIP |
|---|---|---|---|
| Input resolution | 224×224 | 224×224 | 224×224 |
| Pretraining corpus | ImageNet-1K | WIT-400M | WebLI |
| Encoder params | 23.5M | 303.5M | 86.2M |
| Unfrozen layers | layer4 + head | last 1 block + head | last 1 block + head |
| Optimizer | AdamW | AdamW | AdamW |
| Learning rate | 1e-4 | 1e-4 | 1e-4 |
| Weight decay | 1e-4 | 1e-4 | 1e-4 |
| Batch size | 16 | 16 | 16 |
| Max epochs/fold | 20 | 20 | 20 |
| Early-stop metric | Macro-F1 | Macro-F1 | Macro-F1 |
| Patience | 5 | 5 | 5 |
| Val. strategy | 5-fold stratified | 5-fold stratified | 5-fold stratified |
| Threshold grid | 0.01 step | 0.01 step | 0.01 step |
| **Augmentation** | **torchvision** | **torchvision** | **processor only** |
| Approx. epoch time | ~8s | ~480s | ~60–90s |

### Data Augmentation (Training Only)

| Augmentation | ResNet50 | CLIP | SigLIP |
|---|---|---|---|
| Resize 256×256 | ✅ | ✅ | — |
| RandomCrop 224 | ✅ | ✅ | — |
| RandomHorizontalFlip | ✅ | ✅ | — |
| RandomRotation(±15°) | ✅ | ✅ | — |
| ColorJitter | ✅ | ✅ | — |
| RandomGrayscale(10%) | ✅ | ✅ | — |
| RandomErasing(20%) | ✅ | ✅ | — |
| SiglipImageProcessor | — | — | ✅ |

> SigLIP uses only the standard `SiglipImageProcessor` (bilinear resize + normalize). Aggressive augmentation was empirically shown to degrade SigLIP performance, consistent with its sensitivity to distribution shifts from WebLI pretraining.

---

## 📊 Results

### Test Set — Aggregate Metrics (50-image held-out set)

| Metric | ResNet-50 | CLIP ViT-L/14 | SigLIP |
|---|---|---|---|
| **Binary Accuracy** | 0.8186 | 0.9043 | **0.9100** |
| **Hamming Loss** | 0.1814 | 0.0957 | **0.0900** |
| **Micro-F1** | 0.6880 | 0.8269 | **0.8389** |
| **Macro-F1** | 0.5360 | 0.6783 | **0.6878** |

Both vision-language models outperform ResNet-50 by **~15 Macro-F1 percentage points**. The CLIP–SigLIP gap is narrow (0.95 pp on Macro-F1).

### Test Set — Per-Genre F1 Score

| Genre | Support | ResNet-50 | CLIP | SigLIP |
|---|---|---|---|---|
| action | 36 | 0.79 | **0.93** | **0.93** |
| adventure | 22 | 0.70 | 0.89 | **0.91** |
| animation | 8 | 0.93 | 0.84 | **1.00** |
| comedy | 13 | 0.67 | **0.86** | 0.81 |
| crime | 13 | 0.62 | **0.67** | 0.64 |
| drama | 34 | 0.89 | **0.96** | 0.94 |
| family | 4 | **0.44** | 0.40 | 0.40 |
| fantasy | 11 | 0.52 | 0.64 | **0.70** |
| horror | 3 | 0.20 | **1.00** | **1.00** |
| musical | 0 | 0.00 | 0.00 | 0.00 |
| mystery | 13 | 0.47 | **0.63** | 0.50 |
| romance | 1 | 0.00 | 0.00 | 0.00 |
| scifi | 14 | 0.55 | **0.89** | **0.89** |
| thriller | 21 | 0.71 | 0.79 | **0.90** |

> `musical` (0 test positives) and `romance` (1 test positive) score zero across all models — a dataset limitation, not a model failure.

### Cross-Validation (5-Fold) — Macro-F1

| Fold | ResNet-50 @0.5 | ResNet-50 Tuned | CLIP @0.5 | CLIP Tuned | SigLIP @0.5 | SigLIP Tuned |
|---|---|---|---|---|---|---|
| 1 | 0.5546 | 0.6408 | 0.7613 | 0.8180 | 0.7611 | 0.8448 |
| 2 | 0.5727 | 0.6959 | 0.7304 | 0.7999 | 0.7094 | 0.7662 |
| 3 | 0.5534 | 0.6051 | 0.7164 | 0.7609 | 0.7041 | 0.7423 |
| 4 | 0.5198 | 0.5832 | 0.7810 | 0.8173 | 0.7575 | 0.8155 |
| 5 | 0.5153 | 0.6087 | 0.7400 | 0.7770 | 0.6891 | 0.7398 |
| **Mean** | **0.5432** | **0.6267** | **0.7458** | **0.7946** | **0.7242** | **0.7817** |
| **Δ (gain)** | — | **+8.35 pp** | — | **+4.88 pp** | — | **+5.75 pp** |

Threshold calibration provides systematic gains in every fold for every model. ResNet-50 benefits the most in absolute terms because its baseline at threshold=0.5 leaves the largest headroom for minority classes.

---

## 🔑 Final Thresholds (Median Across 5 Folds)

| Genre | ResNet-50 | CLIP ViT-L/14 | SigLIP |
|---|---|---|---|
| action | 0.38 | 0.33 | 0.46 |
| adventure | 0.60 | 0.36 | 0.27 |
| animation | 0.56 | 0.43 | 0.24 |
| comedy | 0.53 | 0.35 | 0.27 |
| crime | 0.41 | 0.61 | 0.39 |
| drama | 0.38 | 0.49 | 0.53 |
| family | 0.67 | 0.38 | 0.43 |
| fantasy | 0.43 | 0.43 | 0.37 |
| horror | 0.47 | 0.43 | 0.16 |
| musical | 0.10 | 0.19 | 0.10 |
| mystery | 0.33 | 0.59 | 0.29 |
| romance | 0.58 | 0.44 | 0.23 |
| scifi | 0.52 | 0.53 | 0.40 |
| thriller | 0.48 | 0.62 | 0.52 |

A consistent pattern: **minority genres receive lower thresholds** because their calibrated probabilities rarely exceed 0.5 for true positives. For example, SigLIP's horror threshold (0.16) is far below CLIP's (0.43), allowing moderate positive signals to cross the decision boundary.

---

## 🔬 Methodology

### 1. Multilabel Stratified K-Fold Cross-Validation
Uses `MultilabelStratifiedKFold` (`iterative-stratification`) to preserve per-label positive proportions across all folds — critical for a 250-image dataset with severe class imbalance where a random split could leave a minority class absent from a fold entirely.

### 2. Class Imbalance Handling with `pos_weight`
`BCEWithLogitsLoss` with per-genre positive weight:
```python
pos_weight[c] = num_negative[c] / num_positive[c]
```
Recomputed **within each fold** from that fold's training split only, so no validation labels influence it. Musical receives weight ≈ 49.0, amplifying its gradient by 49× to prevent the model from ignoring it.

### 3. Dynamic Per-Genre Threshold Calibration
Per-genre threshold grid search over {0.10, 0.11, …, 0.90} maximizing per-class F1 on validation predictions. Final threshold = **element-wise median** across 5 folds (more robust than mean when fold optima vary for rare classes).

### 4. Early Stopping
Monitors val Macro-F1 with patience=5. Saves the best model state (not the final epoch). For the production model (trained on all 250), monitors training loss instead.

### 5. Reproducibility
Seed 42 locked across: Python `random`, NumPy, PyTorch, CUDA. `cudnn.deterministic=True`, `cudnn.benchmark=False`.

---

## 🚀 How to Run

### Step 1 — Prepare Dataset
```
project-akhir/
└── Datasets/
    ├── images/
    │   ├── train/   # 1.jpg – 250.jpg
    │   └── test/    # 251.jpg – 300.jpg
    └── genre.xlsx
```

### Step 2 — Install Dependencies
```bash
pip install torch torchvision open-clip-torch transformers \
            iterative-stratification scikit-learn pandas openpyxl \
            numpy matplotlib seaborn tqdm pillow
```

### Step 3 — Run Notebook
Open one of the notebooks in Jupyter and run cells sequentially:
- `1. project pytorch Resnet50 kvold.ipynb` → ResNet-50
- `2. project pytorch CLIP kfold.ipynb` → CLIP ViT-L/14
- `3. project pytorch siglip-updated.ipynb` → SigLIP

### Step 4 — Outputs
Automatically saved to the `output/` folder in the same directory as the notebook.

---

## 📈 Output Files

| File | Description |
|---|---|
| `submission.csv` | Binary predictions on test set (0/1 per genre) |
| `test_predictions.csv` | Raw probabilities + ground truth labels |
| `thresholds.json` | Optimal per-genre thresholds from K-Fold |
| `cv_fold_metrics_default.csv` | Per-fold metrics at threshold = 0.5 |
| `cv_fold_metrics_tuned.csv` | Per-fold metrics at tuned thresholds |
| `training_history.png` | Training loss curve per epoch |
| `genre_distribution.png` | Genre count distribution + labels-per-movie histogram |
| `genre_cooccurrence.png` | Heatmap of genre co-occurrence pairs |
| `class_imbalance.png` | Positive/negative counts and imbalance ratio per genre |
| `per_genre_performance.png` | Precision/Recall/F1 per genre on test set |
| `prediction_heatmap.png` | Probability heatmap of test set predictions |
| `sample_posters.png` | Sample training posters with their genre labels |
| `sample_predictions.png` | Sample test predictions vs. ground truth |

---

## 💡 Key Findings

### 1. Vision-Language Models Dominate
Both CLIP and SigLIP outperform ResNet-50 by ~15 Macro-F1 percentage points across all metrics. ImageNet pretraining provides limited visual diversity for the typographic, compositional, and stylistic cues that distinguish poster genres. VLMs pretrained on web-scale corpora (WIT-400M, WebLI) transfer those cues more effectively.

### 2. CLIP and SigLIP Are Comparably Strong
The aggregate Macro-F1 gap between them is only 0.95 percentage points on the test set. CLIP actually leads on mean cross-validation tuned Macro-F1 (0.7946 vs 0.7817 for SigLIP). The two models trade leads on individual genres almost equally (4 uniquely for SigLIP, 4 uniquely for CLIP, 3 ties). The 50-image test set introduces sampling variance that comfortably absorbs gaps under 1 percentage point.

### 3. Threshold Calibration Is Universally Beneficial
Per-class threshold calibration via median aggregation over 5 folds yields systematic gains in every fold for every model: **+8.35 pp** for ResNet-50, **+5.75 pp** for SigLIP, **+4.88 pp** for CLIP. This is straightforward to implement and should be considered a standard component of multi-label pipelines on small, imbalanced datasets.

### 4. Key Limitations
- Very small dataset (250 train / 50 test) — high metric variance; a single misclassification on horror (3 positives) shifts F1 by ~33 points
- `musical` (0 test positives) and `romance` (1 test positive) cannot be fairly evaluated — dataset limitation
- CLIP has 3.5× more parameters (303M vs 86M) and uses additional augmentation — controlled comparison isolates architectural differences only partially
- Multi-label genre annotation is inherently subjective

