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

# CODE
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load YOLO
net = cv2.dnn.readNet("path_to_yolov3_weights", "path_to_yolov3_config")

# Loading image
img = cv2.imread("path_to_image")
height, width, channels = img.shape

# Detecting objects
blob = cv2.dnn.blobFromImage(img, 0.00392, (416, 416), (0, 0, 0), True, crop=False)
net.setInput(blob)
output_layers = ["yolo_82", "yolo_94", "yolo_106"]
outs = net.forward(output_layers)

# Showing information on the screen
class_ids = []
confidences = []
boxes = []
for out in outs:
    for detection in out:
        scores = detection[5:]
        class_id = np.argmax(scores)
        confidence = scores[class_id]
        if confidence > 0.5:
            # Object detected
            center_x = int(detection[0] * width)
            center_y = int(detection[1] * height)
            w = int(detection[2] * width)
            h = int(detection[3] * height)

            # Rectangle coordinates
            x = int(center_x - w / 2)
            y = int(center_y - h / 2)

            boxes.append([x, y, w, h])
            confidences.append(float(confidence))
            class_ids.append(class_id)

# Apply NMS
indexes = cv2.dnn.NMSBoxes(boxes, confidences, 0.5, 0.4)

# Draw bounding boxes and labels on the image
font = cv2.FONT_HERSHEY_PLAIN
colors = np.random.uniform(0, 255, size=(len(boxes), 3))
for i in range(len(boxes)):
    if i in indexes:
        x, y, w, h = boxes[i]
        label = str(classes[class_ids[i]])  # Assuming classes are defined
        color = colors[i]
        cv2.rectangle(img, (x, y), (x + w, y + h), color, 2)
        cv2.putText(img, label, (x, y + 30), font, 5, color, 5)  # Increase font size here

# Convert image from BGR to RGB for matplotlib
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Display the image with matplotlib
plt.figure(figsize=(15, 15))  # Increase figure size
plt.imshow(img_rgb)
plt.axis('off')
plt.show()
