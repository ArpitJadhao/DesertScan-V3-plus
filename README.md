# 🌵 DesertScan-V3+: Offroad Semantic Scene Segmentation

**DesertScan-V3+** is a high-performance semantic segmentation solution designed for Unmanned Ground Vehicles (UGVs) navigating challenging desert environments. Built for the **Duality AI Challenge**, it prioritizes high-resolution context and class balance to ensure safe autonomous navigation.

---

## 🚀 Performance Overview
- **Validation mIoU**: `0.5640`
- **Key Successes**: Near-perfect `Sky` (0.9782) and `Trees` (0.8350) detection.
- **Improved Metrics**: Significant IoU gains in minority classes (`Flowers`, `Lush Bushes`) through automated weighting.

---

## 🧠 Technical Architecture
Our solution leverages state-of-the-art architectures optimized for fine-grained feature extraction:
- **Model**: [DeepLabV3+](https://arxiv.org/abs/1802.02611) (Atrous Spatial Pyramid Pooling).
- **Backbone**: `EfficientNet-B3` (Pre-trained on ImageNet).
- **Input Resolution**: **640x640px** (Ensures small obstacles like rocks and logs are detected).
- **Training**: Mixed-Precision (FP16) using `torch.amp` for memory efficiency.

---

## 📁 Dataset & Classes
The model segments the environment into **10 distinct classes**:
1. `Trees` 2. `Lush Bushes` 3. `Dry Grass` 4. `Dry Bushes` 5. `Ground Clutter`
6. `Flowers` 7. `Logs` 8. `Rocks` 9. `Landscape` 10. `Sky`

- **Remapping**: Automated mapping from Falcon simulation IDs (100–10000) to training indices.
- **Augmentation**: Random horizontal/vertical flips, resized crops, and color jitter to improve robustness.

---

## 🛠️ Project Structure
| File | Description |
| :--- | :--- |
| `train.py` | Training script with auto-class weighting and early stopping. |
| `test.py` | Inference script for benchmarks and mask generation. |
| `model.py` | DeepLabV3+ with EfficientNet-B3 implementation. |
| `config.py` | Centralized hyperparameters, paths, and class mappings. |
| `dataset.py` | PyTorch Dataset with advanced augmentations. |
| `utils.py` | Metrics (mIoU), mask remapping, and visualization tools. |

---

## 💻 Getting Started

### 1. Setup Environment
Ensure you are using the `EDU` conda environment:
```powershell
conda activate EDU
```

### 2. Training
Start a new training run:
```powershell
python train.py
```
> [!NOTE]
> Checkpoints and logs are saved automatically to the `runs/` directory.

### 3. Inference & Validation
Generate predictions and an IoU benchmarking report:
```powershell
python test.py
```
The benchmark report will be saved at `runs/iou_report.txt`.

---

## 📊 Visualizations
Predictions and training curves can be found in the `runs/` folder. Use `visualize.py` to inspect specific image-mask pairs.

---
**Challenge Submission - Hackathon 2026**
