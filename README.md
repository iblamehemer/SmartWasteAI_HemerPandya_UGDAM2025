# ♻️ SmartWasteAI – Computer Vision–Based Waste Segregation System

## 1. Project Overview
This project implements an **image-based waste classification and segregation system** for smart cities. The goal is to automatically identify the type of waste from an image and recommend the correct **color-coded disposal bin** (e.g. recyclable, organic, hazardous).  
The solution was developed as part of the **Machine Learning and Deep Learning (AI) Summative Assessment – 2025**.

---

## 2. GitHub Repository Checklist (as per assignment)

- ✅ **All project code/scripts included**:  
  - `app.py`, `train.py`, `bin_logic.py`, `model_utils.py`, `requirements.txt`
- ✅ **Functional GitHub repository**:  
  - [https://github.com/iblamehemer/SA-for-Machine-learning-and-Deep-learning](https://github.com/iblamehemer/SA-for-Machine-learning-and-Deep-learning)
- ✅ **Functional Streamlit link** (to be added after deployment):  
  - `https://<your-app-name>.streamlit.app`
- ✅ **Dataset uploaded**  
  - Dataset folder: `data/`  
  - Structure as required
- ✅ **Trained model included**  
  - `models/waste_classifier.h5`

---

## 3. Research Background / Literature That Influenced the Project
This project is motivated by existing work in **computer vision for solid waste management** and **lightweight CNNs for edge/smart city environments**. Key ideas taken:  
- Waste classification using CNNs – previous studies show that even with limited classes (organic, recyclable, hazardous) a CNN can reach acceptable accuracy for assisting human operators.  
- Use of transfer learning / MobileNetV2 – MobileNet variants are popular for low-compute devices and web apps because they are small, fast and accurate enough for image recognition tasks.  
- Smart city pipeline – camera → classification model → recommendation → dashboard/app. Our Streamlit UI is the “dashboard/app” part.

### References (example list)  
- Sandhu, et al. *“Deep Learning Based Smart Waste Classification.”*  
- Howard, A. et al. **MobileNetV2: Inverted Residuals and Linear Bottlenecks**, Google.  
- Chen, et al. *“Image-based Waste Sorting for IoT-enabled Smart Cities.”*

---

## 4. Dataset and Data Preparation

### 4.1 Dataset Description  
- Total images used (as per training log): **1545 images**  
- Number of classes: **5**  
  - `battery`  
  - `cloth`  
  - `glass`  
  - `metal`  
  - `plastic`

### 4.2 Directory Structure  
```text
data/
  train/
    battery/
    cloth/
    glass/
    metal/
    plastic/
  val/
    ...
  test/
    ...
    4.3 Preprocessing Steps
	•	Images resized to 224×224
	•	Pixel values rescaled to [0,1]
	•	Data augmentation for training:
	•	rotation: 15°
	•	width/height shift: 0.1
	•	zoom: 0.1
	•	horizontal flip: True
	•	Validation data only rescaled

⸻

5. Model Architecture and Training Details

5.1 Model
	•	Base model: MobileNetV2
	•	Input shape: (224, 224, 3)
	•	include_top=False, custom head:
	•	Global Average Pooling
	•	Dense(128, ReLU)
	•	Dense(5, Softmax)
	•	Because of SSL constraints, the model was trained from scratch: weights=None

5.2 Training Parameters
	•	Optimizer: Adam
	•	Loss: categorical_crossentropy
	•	Metrics: accuracy
	•	Epochs: 10
	•	Batch size: 16
	•	Layers of base model frozen

5.3 Training Script
	•	File: train.py
	•	Output: models/waste_classifier.h5

⸻

6. Experimental Results / Metrics

Training log summary:
	•	Images: 1545 across 5 classes
	•	Epochs: 10
	•	Training accuracy: ~26–28%
	•	Validation accuracy: ~27–28%
  Epoch
Train Accuracy
Val Accuracy
Notes
1-3
~0.26-0.27
~0.27-0.28
model initialising from scratch
4-10
~0.27
~0.279
plateau observed due to no pre-trained weights
7. Streamlit Web Application

7.1 File
	•	app.py

7.2 Features
	•	Upload a waste image (JPG/PNG)
	•	Model predicts class: one of [battery, cloth, glass, metal, plastic]
	•	Displays:
	•	Predicted label
	•	Confidence score
	•	Recommended bin via bin_logic.py

7.3 Run Locally
pip install -r requirements.txt
streamlit run app.py
7.4 Deployed App
https://go7qlivlhtwbeyfkdlffpx.streamlit.app

8. Bin Logic (Integration Layer)

bin_logic.py demonstrates system integration: after classification we make a real-world decision.
Example:
def map_class_to_bin(cls):
    recyclable = ["plastic","glass","metal"]
    hazardous = ["battery"]
    organic = ["cloth"]
    if cls in recyclable:
        return "Blue – Recyclable"
    elif cls in hazardous:
        return "Red – Hazardous"
    else:
        return "Green – Biodegradable"
        11. Future Work
	•	Retrain with weights="imagenet" for improved accuracy
	•	Collect larger, more balanced dataset
	•	Add object-detection (e.g., YOLOv8) for multiple items per image
	•	Deploy on Streamlit Cloud and connect to smart-bin IoT hardware

⸻

12. Author / Course Info
	•	Student: Hemer Pandya
	•	School: UGdam
	•	Course: Machine Learning & Deep Learning (Artificial Intelligence)
	•	Assessment: Summative, 2025
	•	GitHub Repo: https://github.com/iblamehemer/SA-for-Machine-learning-and-Deep-learning
	•	Streamlit Link: [(to be added after deployment)](https://go7qlivlhtwbeyfkdlffpx.streamlit.app)
