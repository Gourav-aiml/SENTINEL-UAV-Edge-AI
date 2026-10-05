# SENTINEL – UAV Edge AI Detection System

SENTINEL is an Edge AI based UAV surveillance system designed to perform object detection and basic threat assessment directly on an onboard Raspberry Pi.

The system uses a Raspberry Pi Camera to capture live video, processes the frames using YOLO11n models in ONNX format, and displays detection results and threat information through a Flask-based web dashboard.

## Current Implementation

The current version demonstrates:

* Live camera capture using Raspberry Pi Camera
* Onboard object detection using YOLO11n
* Ground and aerial detection models
* ONNX model inference
* OpenCV DNN based processing
* Rule-based threat assessment
* Flask web dashboard
* Raspberry Pi based Edge AI processing

Autonomous navigation, obstacle avoidance, autonomous landing and direct flight-control commands are outside the current implemented scope and are planned as future extensions.

## System Architecture

```text
Raspberry Pi Camera
        ↓
Raspberry Pi 4B
        ↓
Frame Preprocessing
        ↓
YOLO11n ONNX Model
        ↓
Object Detection
        ↓
Non-Maximum Suppression
        ↓
Threat Assessment
        ↓
Flask Web Dashboard
        ↓
Operator
```

## Hardware

* S500 UAV frame
* Pixhawk 2.4.8 flight controller
* NEO-M8N GPS/compass
* 4 × 2212 920KV motors
* 4 × 30A ESCs
* Raspberry Pi 4B
* Raspberry Pi Camera
* UAV battery and supporting power components

## Software

* Debian GNU/Linux 13 (trixie)
* Python 3.13.5
* OpenCV
* Flask
* NumPy
* YOLO11n
* ONNX model format
* Picamera2

## AI Models

### Ground Model

The ground detection model is based on the YOLO11n model pretrained on the COCO dataset.

### Aerial Model

The aerial detection model is based on YOLO11n and was fine-tuned using the VisDrone dataset to improve object detection for aerial imagery.

The model is exported to ONNX format for Edge AI deployment.

## Detection Pipeline

Each camera frame is captured on the Raspberry Pi and resized to the required model input resolution.

The processed frame is passed to the YOLO11n ONNX model. The model output is decoded and post-processed using confidence filtering and Non-Maximum Suppression.

The resulting detections are passed to the threat assessment module.

## Threat Assessment

The threat assessment module uses rule-based logic to interpret valid object detections.

Detections below the configured confidence threshold are ignored. Valid detections are then used to determine the threat level displayed to the operator.

This module is intended as a simple operator-assistance mechanism and is not presented as a complete operational threat assessment system.

## Dashboard

The Flask dashboard provides:

* Live camera feed
* Detected object information
* Confidence values
* Threat level
* Threat reason
* Environment/status information used for demonstration

## Edge Deployment

The AI inference pipeline is designed to run directly on the Raspberry Pi rather than sending camera frames to a remote computer.

This provides a foundation for low-latency onboard processing and reduces dependence on continuous external connectivity.

## Project Structure

```text
SENTINEL-UAV-Edge-AI/
│
├── README.md
├── LICENSE
├── requirements.txt
│
├── models/
├── src/
├── dashboard/
├── hardware/
├── docs/
└── results/
```

## How to Run

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/SENTINEL-UAV-Edge-AI.git
cd SENTINEL-UAV-Edge-AI
```

Create the Python environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

Run the Flask application:

```bash
python3 src/app.py
```

Open the dashboard from another device on the same network using the Raspberry Pi IP address and the configured Flask port.

## Project Status

### Implemented

* Raspberry Pi camera integration
* YOLO11n object detection
* ONNX model deployment
* OpenCV based inference
* Rule-based threat assessment
* Flask dashboard
* Physical mounting of Raspberry Pi and camera on the S500 platform

### Future Work

* Autonomous navigation
* Obstacle avoidance
* Autonomous landing-zone assessment
* Pixhawk integration for autonomous flight commands
* GPS-denied navigation
* Further aerial-data training and optimization

## Team

SENTINEL is developed as a university project focused on UAV Edge AI, computer vision and autonomous systems.

## License

This project is intended for academic and educational use.
