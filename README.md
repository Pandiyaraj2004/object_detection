# Object Detection

> A browser interface for live YOLOv3 object detection and AI-assisted image descriptions.

**Python · OpenCV DNN · YOLOv3 · Flask · NumPy**

## What it does

- Streams a locally attached webcam into a Flask page.
- Runs YOLOv3 inference with COCO labels and draws bounding boxes.
- Applies confidence filtering and non-maximum suppression.
- Exposes preview, horizontal flip, exposure, contrast, and detection controls.
- Provides a separate image-upload page that requests a description from Gemini.

## How it works

```text
Webcam → OpenCV frame → YOLOv3 → bounding boxes → MJPEG browser stream
Image upload → Flask upload route → Gemini → text description
```

The webcam belongs to the machine running Flask. Detection is toggled through the interface.

## Local setup

```bash
git clone https://github.com/Pandiyaraj2004/object_detection.git
cd object_detection
python -m pip install -r requirements.txt
python -m pip install Pillow google-generativeai
cd models
python dl-weights.py
cd ..
python application.py
```

Open http://localhost:5000. The model downloader writes to its current directory, so run it from `models/`. The app expects `models/yolov3.weights`, alongside the committed configuration and class names.

The upload integration uses a legacy Gemini client and model identifier. Replace the hardcoded credential with your own server-side environment configuration and select an available provider model before using that feature. The two extra packages above are imported by the application but absent from its requirements file.

## Code map

| File | Responsibility |
| --- | --- |
| [application.py](application.py) | Flask routes, upload analysis, camera controls |
| [object_detection.py](object_detection.py) | YOLOv3 inference and video streaming |
| [camera_settings.py](camera_settings.py) | Camera configuration |
| [models](models) | COCO labels, network configuration, weight downloader |
| [templates](templates) | Live detection and upload pages |

## Current limits

Requires a working local camera and downloaded model weights. No inference speed or accuracy benchmark is claimed here. Use as a local demonstration; deployment needs credential handling, upload validation, and production server configuration.

---

Built by **Pandiyaraj A** · [Portfolio](https://pandiyaraj.netlify.app/) · [GitHub](https://github.com/Pandiyaraj2004) · [LinkedIn](https://www.linkedin.com/in/pandiyaraj-a-mca/)
