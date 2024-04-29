# Object-detection-with-YOLO
Using YOLO v3 and YOLO 9000 Object detection model
# YOLO (You Only Look Once)

## Overview

This project implements the YOLO (You Only Look Once) object detection algorithm using OpenCV and Python. YOLO is a state-of-the-art, real-time object detection system that can detect multiple objects in an image with high accuracy and speed.

## Requirements

- Python 3.x
- OpenCV
- Pre-trained YOLO model weights and configuration file

## Installation

1. Clone the repository:

    ```
    git clone https:https://github.com/intellecual/Object-detection-with-YOLO
    ```

2. Install dependencies:

    ```
    pip install opencv-python
    ```

3. Download pre-trained YOLO model weights and configuration file from [YOLO website](https://pjreddie.com/darknet/yolo/) and place them in the project directory.

## Usage

1. Run the `yolo_detection.py` script:

    ```
    python yolo_detection.py --image <image_path>
    ```

    Replace `<image_path>` with the path to the image you want to perform object detection on.

2. View the detected objects in the output image.

## Options

- `--image`: Path to the input image for object detection.
- `--video`: Path to the input video for object detection (optional).
- `--output`: Path to save the output image or video (optional).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- YOLO: Real-Time Object Detection (https://pjreddie.com/darknet/yolo/)
