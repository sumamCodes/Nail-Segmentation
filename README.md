# Nail Segmentation and Measurement Pipeline

This project focuses on accurately segmenting and measuring nails in images using computer vision techniques. The goal was to build a reliable pipeline that could segment nails and provide precise length measurements.

## 📌 Project Overview

The process followed a progressive refinement approach:
1. **Segmentation with YOLOv8**
2. **Measurement Estimation from Segmentation Masks**
3. **Depth Estimation using MiDaS**
4. **Reference Object-based Measurement for Accuracy**
5. **Deployment in Flutter using TFLite**

---

## 🧠 Step-by-Step Process

### 1. Data Collection and Preprocessing
- Collected and annotated nail segmentation data using **Roboflow**.
- The dataset included **pixel-wise segmentation masks** for each nail, suitable for training semantic segmentation models.

### 2. Nail Segmentation using YOLOv8
- Trained a **YOLOv8 segmentation model** on the Roboflow dataset.
- The model produced **binary masks** highlighting the nail regions in each input image.
- Provided good visual segmentation results across varied image conditions.

### 3. Measurement Estimation from Segmentation Masks
- Attempted to calculate nail length by analyzing the pixel dimensions of segmented regions.
- However, due to lack of scale calibration, **measurements were inaccurate** and inconsistent across images.

### 4. Depth-Based Measurement with MiDaS
- Integrated the **MiDaS depth estimation model** to generate relative depth maps.
- Tried to leverage depth data to infer real-world scale of the segmented nails.
- This method improved relative understanding of shape and perspective, but still **failed to provide accurate physical measurements** due to absence of absolute scale.

### 5. Reference Object-based Measurement
- Introduced a **reference object of known dimensions** (e.g., ruler or coin) in each image.
- Computed a **pixel-to-length ratio** from the reference, then applied it to segmented nail masks for accurate length estimation.
- This method proved to be the **most effective and reliable**.

### 6. Model Conversion for Mobile Deployment
- Converted the trained **YOLOv8 segmentation model to TFLite** format using ONNX and TensorFlow Lite tools.
- Successfully deployed the model in a **Flutter mobile application** for real-time, on-device nail segmentation and measurement.

---

## 📱 Tech Stack

- **Model Training**: Python, PyTorch, YOLOv8 (Segmentation)
- **Depth Estimation**: MiDaS (Vision Transformers)
- **Annotation & Preprocessing**: Roboflow
- **Model Conversion**: ONNX → TensorFlow → TFLite
- **Mobile Integration**: Flutter, TFLite

---

## ✅ Conclusion

This project demonstrates an end-to-end pipeline for nail segmentation and measurement, evolving from simple segmentation to accurate, real-world scaling using a reference object. Despite the potential of depth-based methods, reliable measurements were only achieved with reference calibration. The final model was successfully optimized and integrated into a mobile app using Flutter and TFLite.
