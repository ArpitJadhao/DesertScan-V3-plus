# Offroad Semantic Scene Segmentation - Duality AI Challenge

This repository contains the source code, training configurations, and benchmarking scripts for the Offroad Autonomy Segmentation challenge. Our solution utilizes a DeepLabV3+ architecture with a high-capacity encoder to accurately segment desert environments for Unmanned Ground Vehicles (UGVs).

## 📊 Final Performance
- **Validation mIoU**: 0.5640
- **Best Classes**: Sky (0.9782), Trees (0.8350), Lush Bushes (0.6932)
- **Top Improvement**: Upgraded from EfficientNet-B1 to B3, increasing resolution to 640px.

## 🛠️ Project Structure
- `train.py`: Main training script with automated class weight computation.
- `test.py`: Inference script for generating predictions and validation benchmarks.
- `model.py`: Model architecture definitions (DeepLabV3+ with EfficientNet-B3).
- `config.py`: Global hyperparameters and class mappings.
- `dataset.py`: PyTorch dataset implementations for training and testing.
- `utils.py`: Utility functions for remapping masks, computing IoU, and visualizing results.
- `runs/`: Directory containing checkpoints, loss curves, and predictions.

## 🚀 Getting Started

### 1. Requirements
Ensure you have the `EDU` environment set up as per the hackathon instructions using the provided `setup_env.bat`.

### 2. Training
To train the model from scratch:
```powershell
conda activate EDU
python train.py
```
Training logs and the best model checkpoint will be saved to the `runs/` directory.

### 3. Inference & Benchmarking
To generate predictions for the test images and view the validation report:
```powershell
python test.py
```
- **Predictions**: Saved in `runs/predictions/`
- **IoU Report**: Saved as `runs/iou_report.txt`

## 🧠 Key Optimizations
1. **Backbone Upgrade**: Transitioned to `efficientnet-b3` for superior feature extraction.
2. **Resolution Scaling**: Increased input size to **640x640** pixels to capture finer details of small objects like rocks and logs.
3. **Imbalance Handling**: Automated inverse-frequency class weighting to assist the model in learning minority classes.
4. **Auto-Casting**: Used `torch.amp` for mixed-precision training to optimize memory usage on higher resolutions.

## 📁 Submission Requirements
- **Model Weights**: Located at `runs/best_model.pth`
- **Output Report**: See `runs/iou_report.txt`
- **Predictions**: Color-mapped masks in `runs/predictions/`
