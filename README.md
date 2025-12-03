# 🍽️ Food Image Classification Using CNN & Transfer Learning

## **1. Overview**

This project develops and compares four deep learning models for classifying 20 food categories from a curated subset of Food-101:

1. Vanilla CNN (no augmentation)
2. CNN with data augmentation
3. Transfer Learning using Xception
4. Transfer Learning + Augmentation

The objective is to understand how data augmentation and transfer learning affect performance, training efficiency, and generalization.

## **2. Dataset**

* Source: Food-101 (20 selected classes, 1,000 images/class)
* Total images: 20,000
* Split:

  * Train: 16,000
  * Validation: 2,000
  * Test: 2,000
* Image sizes:

  * CNN: 224×224×3
  * Xception: 299×299×3

Dataset description from the ppt.

## **3. Model Summary**

### **3.1 Vanilla CNN**

* 4 convolutional blocks (32→64→128→256 filters)
* BatchNorm + MaxPooling + Dropout
* GlobalAveragePooling + Dense(256→128) + Softmax(20)
* Optimizer: AdamW
* Regularization: L2, Label Smoothing, Mixed Precision

### **3.2 CNN + Data Augmentation**

* Augmentations: rotation, shear, zoom, shift, brightness, color jitter, flips
* 4 deeper blocks (64→512 filters, 3 conv/layer)
* One-cycle LR schedule, AdamW

### **3.3 Xception (Transfer Learning)**

* Pretrained on ImageNet
* Two-stage training:

  * Feature Extraction → train custom head only
  * Fine-tuning → unfreeze top ~100 layers
* Dense head: GAP → 512 → 256 → Softmax

### **3.4 Xception + Augmentation**

* Same augmentation as 3.2
* Parameter summary:

  * Total: ~22M
  * Trainable: ~1.19M
  * Non-trainable: ~20.86M

Figures and architecture details from pages 20–33 of the report .

## **4. Results**

| Model          | Acc        | Prec       | Recall     | F1         |
| -------------- | ---------- | ---------- | ---------- | ---------- |
| CNN            | 0.8135     | 0.8163     | 0.8135     | 0.8123     |
| CNN + Aug      | 0.8450     | 0.8525     | 0.8450     | 0.8458     |
| Xception       | 0.8780     | 0.8806     | 0.8780     | 0.8784     |
| Xception + Aug | **0.9025** | **0.9043** | **0.9025** | **0.9029** |

**Key takeaway:** Transfer learning provides the largest performance boost, while augmentation further strengthens generalization.

## **5. Conclusion**

* Pretrained Xception significantly outperforms CNN trained from scratch.
* Data augmentation reduces overfitting and improves robustness.
* The best configuration: **Transfer Learning + Augmentation**.
* Suitable for food recognition applications such as nutrition estimation, menu digitization, and culinary analytics.

# 🇻🇳 **(VI)**

## **1. Tổng quan**

Dự án xây dựng và so sánh bốn mô hình phân loại ảnh món ăn (20 lớp) từ tập Food-101:

1. CNN cơ bản
2. CNN + tăng cường dữ liệu
3. Transfer Learning với Xception
4. Transfer Learning + Augmentation

Mục tiêu là đánh giá tác động của augmentation và transfer learning lên hiệu suất mô hình.

## **2. Bộ dữ liệu**

* Nguồn: Food-101 (20 lớp, 1.000 ảnh mỗi lớp)
* Tổng số ảnh: 20.000
* Chia tập:

  * Train: 16.000
  * Val: 2.000
  * Test: 2.000
* Kích thước ảnh: 224×224×3 hoặc 299×299×3

## **3. Mô hình**

### **3.1 CNN cơ bản**

* 4 block tích chập (32→256)
* BatchNorm + Pooling + Dropout
* GAP → Dense(256→128) → Softmax(20)
* AdamW, L2, Label Smoothing

### **3.2 CNN + Augmentation**

* Xoay, dịch, shear, zoom, tăng sáng, biến đổi màu, lật
* Kiến trúc sâu hơn (64→512)

### **3.3 Xception (Transfer Learning)**

* Pretrained ImageNet
* Huấn luyện 2 giai đoạn
* Head: GAP → 512 → 256 → Softmax

### **3.4 Xception + Augmentation**

* ~22M tham số, trong đó trainable ~1.19M

## **4. Kết quả**

| Model          | Acc        | Prec       | Recall     | F1         |
| -------------- | ---------- | ---------- | ---------- | ---------- |
| CNN            | 0.8135     | 0.8163     | 0.8135     | 0.8123     |
| CNN + Aug      | 0.8450     | 0.8525     | 0.8450     | 0.8458     |
| Xception       | 0.8780     | 0.8806     | 0.8780     | 0.8784     |
| Xception + Aug | **0.9025** | **0.9043** | **0.9025** | **0.9029** |

**Kết luận chính:** Transfer Learning cải thiện mạnh nhất; augmentation tăng khả năng khái quát.

## **5. Kết luận**

* Xception vượt trội so với CNN tự huấn luyện.
* Augmentation giảm overfitting.
* Mô hình tốt nhất: **Xception + Augmentation**.
* Phù hợp cho ứng dụng nhận diện món ăn, gợi ý dinh dưỡng, phân tích hình ảnh ẩm thực.
