# Deteksi-Bola-Roboflow

 # Jawaban

```python
# Step 1: Install necessary libraries
!pip install ultralytics  # Install YOLOv8
!pip install matplotlib opencv-python-headless
!pip install roboflow

# Step 2: Import libraries
import matplotlib.pyplot as plt
from ultralytics import YOLO
from google.colab import files
import cv2
import numpy as np

from roboflow import Roboflow
rf = Roboflow(api_key="uuSym5k4bB2YSX3RkixW")
project = rf.workspace("uas-pengolahan-citra-digital").project("ball-auto-dataset")
version = project.version(1)
dataset = version.download("yolov8")

# Lihat folder tempat dataset diunduh
dataset_location = dataset.location  # dari RoboFlow download
print("Dataset downloaded to:", dataset_location)

from ultralytics import YOLO
# Buat model YOLOv8 baru
model = YOLO("yolov8n.pt")  # "yolov8n.pt" adalah versi YOLOv8 Nano
# Jalankan pelatihan dengan dataset
model.train(data="/content/Ball-auto-dataset-1/data.yaml", epochs=100, imgsz=320)

# Step 3: Upload image
uploaded = files.upload()
image_path = list(uploaded.keys())[0]

# Step 4: Perform object detection
results = model(image_path)  # Run inference on the uploaded image

# Step 5: Visualize results
# Save the annotated image
annotated_img = results[0].plot()
plt.figure(figsize=(10, 10))
plt.imshow(cv2.cvtColor(annotated_img, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.show()

```
