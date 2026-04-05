# 🌱 AgroKD-Net: Distilled & Lightweight YOLOv11n for Weed Detection

## 📌 Overview

This project presents a **distilled and lightweight YOLOv11n-based object detection model** for **weed detection in precision agriculture**, optimized for **edge devices** such as robots and smart tractors.

We leverage:

* 🔁 **Channel-wise Knowledge Distillation (CWD)**
* 📊 **Supervised Learning with Ground Truth Labels**
* ⚡ **Model Compression for Efficiency**

---

## 🧠 Motivation

Deploying deep learning models in agriculture requires:

* Low **latency**
* Low **energy consumption**
* High **accuracy**

To address this, we compress a **YOLOv11n teacher model** into a **lightweight student model** while preserving performance using knowledge distillation.

---

## 🏗️ Model Architecture

### 🔷 Teacher Model (YOLOv11n)

* Parameters: **2.58M**
* GFLOPs: **6.3**
* Model Size: **5.50 MB**
* Role: Provides **feature-level supervision**

---

### 🟩 Student Model (Light YOLOv11n)

* Parameters: **1.49M**
* GFLOPs: **5.4**
* Model Size: **3.07 MB**
* Modification:

  * Reduced max channels (**1024 → 512**)
  * Same depth & width scaling factors

---

## 🔁 Knowledge Distillation Strategy

We apply **Channel-Wise Distillation (CWD)** on:

* 📍 Layer 16 (P3 - Small objects)
* 📍 Layer 19 (P4 - Medium objects)
* 📍 Layer 22 (P5 - Large objects)

* <img width="940" height="499" alt="image" src="https://github.com/user-attachments/assets/1b2ec75c-fa33-4ae7-ae82-792693d86a4a" />

---

## 📉 Loss Functions

### 🔹 Supervised Loss

```math
L_s = \text{YOLO Detection Loss}(pred_s, GT)
```

Includes:

* Classification Loss
* Bounding Box Loss (IoU)
* Distribution Focal Loss

---

### 🔹 Distillation Loss (CWD)

```math
L_{KL}(p||q) = - \sum p(x) \log \frac{p(x)}{q(x)}
```

* Based on **KL-Divergence**
* Temperature: **T = 3.5**

---

### 🔹 Total Loss

```math
L_{total} = L_s + \alpha L_{KL}
```

* α (distillation weight): **0.05**

---

## ⚙️ Training Setup

| Parameter       | Value     |
| --------------- | --------- |
| Epochs          | 100       |
| Batch Size      | 16        |
| Image Size      | 640 × 640 |
| Optimizer       | AdamW     |
| Learning Rate   | 0.01      |
| Weight Decay    | 0.0005    |
| Train/Val Split | 70% / 30% |

---

## 📊 Results

### 🔍 Teacher vs Student

| Metric     | Teacher | Student |
| ---------- | ------- | ------- |
| GFLOPs     | 6.3     | 5.4     |
| Parameters | 2.58M   | 1.49M   |
| Model Size | 5.50 MB | 3.07 MB |
| Precision  | 0.89    | 0.79    |
| Recall     | 0.84    | 0.79    |
| mAP@50     | 0.90    | 0.83    |
| mAP@50-95  | 0.86    | 0.77    |

---

### 📈 Benchmark Comparison

| Model                     | Params    | GFLOPs  | mAP@50   |
| ------------------------- | --------- | ------- | -------- |
| YOLOv11n                  | 2.58M     | 6.45    | 0.909    |
| YOLOv8n                   | 3.00M     | 8.09    | 0.921    |
| RT-DETR Lite              | 32.8M     | 108     | 0.041    |
| YOLOv8s                   | 11.1M     | 28.6    | 0.943    |
| YOLOv7-tiny               | 6.04M     | 13      | 0.859    |
| **Light YOLOv11n (Ours)** | **1.49M** | **5.4** | **0.83** |

---
<img width="940" height="259" alt="image" src="https://github.com/user-attachments/assets/1103dd15-2296-4a11-aca5-46f250389897" />
<img width="940" height="277" alt="image" src="https://github.com/user-attachments/assets/091a19ca-28cd-4efd-bdc6-a2055da341cb" />

## ⚡ Performance Gains

* 🔻 **Parameters reduced by ~42%**
* 🔻 **GFLOPs reduced by ~16%**
* 🔻 **Model size reduced by ~44%**
* ⚡ **Latency improved by ~14%**
* ✅ Maintains **mAP ≥ 0.8**

---

## 🚜 Applications

* Autonomous weed detection
* Smart farming robots
* Edge AI in agriculture
* Real-time crop monitoring

---

## 🔮 Future Work

* Masked Generative Distillation (MGD)
* Hybrid KD methods
* Deployment on embedded systems (Jetson, Edge TPU)
* Evaluation on diverse agricultural datasets

---

## 👤 Author

**Suvidha Foundation & Team**

---

## 📜 License

MIT License
