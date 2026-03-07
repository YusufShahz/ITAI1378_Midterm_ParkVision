# ParkVision – Parking Lot Occupancy Detector

**Student:** Yusuf Shahzad  
**Course:** ITAI 1378 – Computer Vision & AI  
**Tier:** Tier 2 – Object Detection

---

## Problem Statement
Drivers waste significant time circling parking lots with no visibility
into which spaces are available. This causes traffic congestion,
fuel waste, and frustration for drivers and lot operators alike.

## Solution Overview
ParkVision uses YOLOv8 to analyze overhead camera images of parking
lots and classify each space as occupied or empty in real time,
generating a visual overlay and availability count.

## Technical Approach
- **CV Technique:** Object Detection
- **Model:** YOLOv8n / YOLOv8s (Ultralytics)
- **Framework:** PyTorch + Ultralytics
- **Input:** Overhead parking lot images (640×640)
- **Output:** Bounding boxes + occupied/empty classification

## Dataset
- **Source:** PKLot via Roboflow Universe
- **Size:** ~12,000 labeled images
- **Classes:** `occupied`, `empty`
- See [data/README.md](data/README.md) for download instructions

## Success Metrics
| Metric | Target |
|--------|--------|
| Detection Accuracy | ≥ 90% |
| mAP@0.5 | ≥ 85% |
| Inference Speed | < 1s per frame |
| False Negatives | < 5% |

## Week-by-Week Plan
| Week | Task | Milestone |
|------|------|-----------|
| 10 | Dataset setup, repo, Colab env | Dataset ready |
| 11 | Train YOLOv8 baseline | Model running |
| 12 | Augmentation + fine-tuning | ≥90% accuracy |
| 13 | Visual overlay + demo video | Demo ready |
| 14 | Docs, README, final report | Fully documented |
| 15 | Present | 🎉 Done |

## Resources
| Resource | Tool | Cost |
|----------|------|------|
| Compute | Google Colab / Kaggle | $0 |
| Model | Ultralytics YOLOv8 | $0 |
| Dataset | PKLot via Roboflow | $0 |
| Annotation | LabelImg (if needed) | $0 |

## Risks & Mitigation
| Risk | Probability | Mitigation |
|------|-------------|------------|
| Low accuracy on occluded cars | Medium | Data augmentation, try YOLOv8m |
| Dataset mismatch | Medium | Supplement with Roboflow dataset |
| Colab GPU quota | Low | Switch to Kaggle notebooks |
| Overfitting | Medium | Early stopping, dropout |

## AI Usage Log
| Date | Tool | How it was used |
|------|------|-----------------|
| March 6 | Claude | Generated project proposal and slide deck |
