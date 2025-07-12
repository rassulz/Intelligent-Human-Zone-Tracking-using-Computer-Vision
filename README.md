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
