# 🅿️ ParkVision – Parking Lot Occupancy Detector

## 🎥 Demo Video
[Watch Demo](https://drive.google.com/file/d/1ykO3VyCKquqZq0wyWLtg77qWCP6DKBPy/view?usp=sharing)

---

## Team Members
- Yusuf Shahzad – Solo Project (All roles)

## Project Tier
**Tier 2** – Object Detection with YOLOv8. Tier 2 because it uses bounding box detection across ~12,000 images with a custom-trained model, not just classification.

---

## 🎯 Problem & Solution

### The Problem
Drivers waste an average of 8 minutes per trip circling parking lots with no visibility into which spaces are available. This causes 30% of urban traffic congestion and costs an estimated $97 billion annually in wasted fuel and time.

### Our Solution
ParkVision uses a fine-tuned YOLOv8s model to analyze overhead parking lot camera images and classify each space as occupied or empty in real time, generating a color-coded visual overlay and live availability count.

### Impact
Parking lot operators and drivers both benefit — operators can display real-time availability on signage, while drivers can route directly to open spaces. The system runs at 17ms per frame, fast enough for live camera feeds.

---

## 🔧 Technical Details

### Approach
- **Task**: Object Detection
- **Model**: YOLOv8s (Ultralytics)
- **Framework**: PyTorch 2.0 + Ultralytics
- **Key Libraries**: ultralytics, opencv-python, roboflow, matplotlib

### System Architecture
[Overhead Camera Image 640×640]
↓
[Preprocessing: Resize + Normalize RGB]
↓
[YOLOv8s Detection Model – 73 layers]
↓
[Classify each box: occupied / empty]
↓
[Visual Overlay: Red/Green boxes + HUD count]
---

## 📊 Dataset
- **Source:** [PKLot via Roboflow Universe](https://universe.roboflow.com/sagitova-aliya/pklot-qesrf)
- **Size:** ~12,000 labeled images
- **Classes:** `occupied`, `empty`
- **Split:** Train: 70% | Val: 15% | Test: 15%
- **Preprocessing:** Auto-resize to 640×640, RGB normalization, horizontal flip augmentation

See [data/README.md](data/README.md) for download instructions.

---

## 🚀 How to Run

### Installation
```bash
git clone https://github.com/YusufShahz/ITAI1378_Midterm_ParkVision.git
cd ITAI1378_Midterm_ParkVision
pip install -r requirements.txt
```

### Quick Start
```bash
# Run the interactive demo notebook
jupyter notebook notebooks/04_demo.ipynb
```

### Detailed Usage
Open notebooks in order:
1. `01_data_exploration.ipynb` – Verify dataset and visualize samples
2. `02_model_training.ipynb` – Train YOLOv8s (requires GPU)
3. `03_evaluation.ipynb` – Run full metrics and confusion matrix
4. `04_demo.ipynb` – Visual demo with green/red overlay

Pre-trained model weights: [Download best.pt from Google Drive](YOUR_DRIVE_LINK_HERE)

---

## 📈 Results

| Metric | Target | **Achieved** |
|--------|--------|-------------|
| mAP@0.5 | ≥ 85% | **99.5%** |
| Precision | — | **99.8%** |
| Recall | — | **99.8%** |
| Inference Speed | < 1s | **~17ms (57× faster)** |

### Success Cases
The model correctly classifies occupied and empty spaces even with partial occlusion and varying lighting conditions across all test images.

### Failure Cases / Limitations
- Performance on parking lots with very different camera angles (not in PKLot) is untested
- Night-time or low-light scenarios may reduce accuracy without retraining on augmented data

### Comparison with Baseline

| Approach | mAP@0.5 | Speed |
|----------|---------|-------|
| Manual inspection | N/A | Minutes |
| Simple color threshold | ~40% | <0.01s |
| **ParkVision (YOLOv8s)** | **99.5%** | **17ms** |

---

## 💡 Key Learnings

### What Worked Well
- YOLOv8s fine-tuned extremely fast on PKLot — hit 97.7% mAP on the very first epoch
- Roboflow made dataset download and formatting for YOLOv8 trivially easy
- Google Colab T4 GPU was sufficient for the entire project at no cost

### Challenges Faced
- **Challenge:** Understanding why accuracy was so high from epoch 1
- **Solution:** Realized YOLOv8 comes pre-trained on COCO which already understands cars — PKLot fine-tuning is essentially transfer learning, not training from scratch
- **Challenge:** Colab session resets losing all data
- **Solution:** Mounted Google Drive and saved all checkpoints after each session

### What I'd Do Differently
- Add a real-time video stream demo using OpenCV VideoCapture
- Test generalization on parking lots not in the PKLot dataset
- Build a simple web interface using Gradio or Streamlit

---

## 🤖 AI Usage Documentation

See detailed log: [docs/AI_usage_log.md](docs/AI_usage_log.md)

**Summary:**
- Used AI for: project ideation, code generation, slide creation, debugging, result interpretation
- Key learnings: AI helped accelerate setup but understanding each notebook cell was still required
- Code attribution: ~40% written/modified by me, ~60% AI-generated and reviewed/tested by me

---

## 🔮 Future Improvements
1. **Real-time video stream** – Integrate with OpenCV to process live RTSP camera feeds
2. **Web dashboard** – Build a Gradio or Streamlit UI showing lot availability in real time
3. **Multi-lot support** – Handle multiple camera angles and parking configurations
4. **Night mode** – Retrain with low-light augmentation for 24/7 operation

---

## 📚 References
1. [Ultralytics YOLOv8 Documentation](https://docs.ultralytics.com)
2. [PKLot Dataset – Roboflow](https://universe.roboflow.com/sagitova-aliya/pklot-qesrf)
3. [Original PKLot Paper – UFPR](https://web.inf.ufpr.br/vri/databases/parking-lot-database/)
4. [PyTorch Documentation](https://pytorch.org/docs/stable/index.html)

---

## 📄 License
Academic Use Only – ITAI 1378 Course Project

## 🙏 Acknowledgments
- Professor for course guidance and project structure
- Ultralytics for the open-source YOLOv8 framework
- Roboflow for dataset hosting and formatting tools
- Claude (Anthropic) for AI assistance throughout the project
