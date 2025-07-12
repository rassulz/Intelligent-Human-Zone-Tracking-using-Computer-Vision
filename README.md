````markdown
# Intelligent Human-Zone Tracking using Computer Vision

A real-time safety monitoring system for hazardous industrial zones that detects people, verifies safety-vest compliance, and tracks dwell-time in danger areas—raising instant alerts when safety rules are violated.

---

## 🚀 Features

- **Human Detection**  
  Frame-by-frame person detection powered by YOLOv8 for high speed and accuracy.

- **Safety-Vest Classification**  
  Color-based vest presence check:  
  - ❌ **No Vest** → Immediate **RED** alert  
  - 🟡 **Yellow Vest** → Start zone-timer & issue **YELLOW** warning if threshold exceeded

- **Zone-Based Timer**  
  Tracks how long each person remains in the danger zone; configurable time limits trigger audible/visual warnings.

- **(Optional) Face Recognition**  
  Integrate dlib-based face matching to tag and log individual IDs in the dashboard.

- **Web Dashboard**  
  Flask-powered UI to stream video, display alerts, timers, and safety logs in real time.

---

## 📦 Getting Started

### Prerequisites

- Python 3.8+  
- CUDA-enabled GPU (recommended for real-time performance)  
- [Roboflow Dataset: Safety Vests](https://universe.roboflow.com/zhanibek/safety-vests-wz02d/dataset/1)  

### Installation

1. **Clone this repository**  
   ```bash
   git clone https://github.com/your-username/human-zone-tracking.git
   cd human-zone-tracking
````

2. **Create & activate a virtual environment**

   ```bash
   python3 -m venv venv
   source venv/bin/activate     # Linux/macOS
   venv\Scripts\activate.bat    # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

---

## ⚙️ Usage

1. **Download or link your dataset**

   * Export your annotated images from Roboflow (YOLO format).
   * Place `train/`, `val/`, `test/` folders under `data/safety_vests/`.

2. **Train YOLOv8 model** (optional)

   ```bash
   yolo detect train model=yolov8n.yaml data=data/safety_vests/ epochs=50 imgsz=640
   ```

3. **Run inference & dashboard**

   ```bash
   python app.py \
     --weights runs/train/exp/weights/best.pt \
     --source 0 \
     --zone-file config/zone.json \
     --time-threshold 10
   ```

   * `--source` can be a webcam index or video file.
   * `--zone-file` defines polygon(s) of hazardous area(s).
   * `--time-threshold` is the max seconds allowed in-zone with a vest.

---

## 📊 Results & Demo

* **Detection accuracy:** mAP₅₀ > 92%
* **Real-time performance:** ≈25 FPS on RTX 2060
* **Demo Video:** [YouTube Link](https://youtu.be/your-demo-link)

![Dashboard Screenshot](docs/dashboard_screenshot.png)

---

## 🛠️ Project Structure

```
├── app.py                 # Main Flask app + inference loop  
├── models/                # YOLOv8 model configs & weights  
├── data/                  # Train/Val/Test datasets  
│   └── safety_vests/      
├── utils/
│   ├── detector.py        # YOLOv8 wrapper
│   ├── vest_classifier.py # Color-based vest check
│   ├── timer.py           # Zone dwell-time logic
│   └── face_recog.py      # (Optional) dlib integration
├── requirements.txt
└── README.md
```

---

## 📝 Configuration

* **`config/zone.json`**

  ```json
  {
    "zone_polygon": [[x1,y1], [x2,y2], …, [xn,yn]]
  }
  ```
* **`config/settings.yaml`**

  ```yaml
  time_threshold: 10       # seconds
  alert_colors:
    no_vest: "red"
    vest:    "yellow"
  ```

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m "Add YourFeature"`)
4. Push to branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

Please adhere to the existing coding style and include tests for new functionality.

---

## 👥 Team & Acknowledgments

* **Rasul & Zhanibek** – YOLOv8 human & vest detection
* **Olzhas & Bakkustar** – Face-recognition module
* **Ilyas** – Zone timer & alert logic

Special thanks to [Roboflow Universe Dataset](https://universe.roboflow.com/zhanibek/safety-vests-wz02d/dataset/1) for annotated safety-vest images.

---
