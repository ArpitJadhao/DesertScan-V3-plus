# Offroad Autonomy Semantic Segmentation: Hackathon Report
**Team Name**: Team DesertSeg
**Score (Val mIoU)**: 0.5640

---

## 1. Methodology
Our approach focused on leveraging **Transfer Learning** and **Resolution Scaling** to overcome the complexities of off-road desert environments.

### Data Preparation
- **Remapping**: Converted raw simulation IDs (e.g., 7100 for Landscape) to sequential training indices.
- **Augmentation**: Implemented horizontal flipping and perspective shifts to simulate varied camera angles on rugged terrain.
- **Normalization**: Standardized RGB inputs to Match Imagenet statistics for pre-trained weights.

### Model Architecture
We selected **DeepLabV3+** due to its Atrous Spatial Pyramid Pooling (ASPP), which captures features at multiple scales—essential for detecting both distant trees and near-field rocks.
- **Encoder**: Upgraded from EfficientNet-B1 to **EfficientNet-B3** to expand feature representation.
- **Input Size**: Scaled to **640x640** pixels.

---

## 2. Results & Performance
The model achieved a final **Val mIoU of 0.5640**.

| Class | IoU | Observation |
| :--- | :--- | :--- |
| **Sky** | 0.9782 | Near perfect classification due to high contrast. |
| **Trees** | 0.8350 | Robust detection of large vertical structures. |
| **Flowers** | 0.6151 | Successfully localized small magenta regions. |
| **Rocks** | 0.3498 | Struggles with texture similarity to the ground. |
| **Logs** | 0.1582 | Most difficult class due to occlusion and sand coverage. |

### Visual Insights
- **Success Case**: High accuracy on clear borders (Sky-Landscape-Trees).
- **Metric Trends**: Loss steadily decreased over 80 epochs, with early stopping triggering at epoch 45, preserving generalization.

---

## 3. Challenges & Solutions

### Problem: Severe Class Imbalance
Classes like "Logs" and "Rocks" are significantly underrepresented compared to "Landscape" and "Sky".
- **Initial Result**: Model ignored logs entirely (0.0 IoU).
- **Solution**: Implemented **Inverse Frequency Class Weights** in the CrossEntropy loss function to "penalize" the model more for missing rare classes.

### Problem: Fine-Detail Retrieval
At 512px resolution, small terrain objects were blurred into the sand.
- **Solution**: Increased resolution to 640px and switched to a deeper decoder. This increased mIoU by ~3%.

---

## 4. Failure Case Analysis
The primary failure mode is the confusion between **Logs/Rocks** and **Landscape**. 

**Observations**:
- Logs are often partially buried in sand or placed in the shadow of bushes.
- The model tends to label these as "Landscape" because their spectral profile is highly similar to sand.
- **Future Work**: Implementing *OHEM (Online Hard Example Mining)* or utilizing *Temporal Consistency* across frames could help distinguish these permanent objects from shiftable sand.

---

## 5. Conclusion
By combining a modern segmentation architecture with targeted hyperparameter tuning and class weighting, we established a robust baseline for off-road autonomy. The use of high-quality synthetic data from Duality AI allowed us to iterate rapidly and focus on specialized class imbalance challenges.
