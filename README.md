# CIFAR-10 CNN Classifier

This repository contains a **Convolutional Neural Network (CNN)** implementation for **multi-class image classification** on the CIFAR-10 dataset. The model is optimized for efficient training and performance on the CIFAR-10 image resolution of **32x32 pixels**.

---

## Data Preprocessing Pipeline

### 1. Image Size Selection
- **Chosen Resolution**: **32x32 pixels**, the native resolution of CIFAR-10.
- **Rationale**:
  - Achieves **optimal accuracy** (72%) compared to larger resolutions like 64x64 (69%) and 128x128, which added unnecessary computation.
  - Avoids **interpolation artifacts** that arise when resizing to higher resolutions, preserving image features.
  - **More efficient training** with lower computational requirements, especially useful for quick experimentation.

### 2. Data Augmentation Techniques
Using TensorFlow's `ImageDataGenerator`, several augmentation techniques were applied to improve the model's ability to generalize:
- **Rotation (15°)**: Allows the model to handle slight orientation changes in images.
- **Width/Height Shifts (10%)**: Provides **position invariance**, improving the model's performance across shifted images.
- **Horizontal Flip**: Doubles the effective dataset size and introduces variability, reducing the risk of overfitting.

### 3. Normalization
- **Method**: Pixel values are scaled to [0,1] by dividing by 255.0.
- **Importance**: Ensures **stable training**, improves **gradient flow**, and enhances **model convergence** by placing all input values on a similar scale.

### 4. Image Integrity Checks
- Included **corruption detection** to ensure data quality, promoting **consistent training results**.

---

## Model Architecture

### 1. Convolutional Layers
```python
Conv2D(32, (3, 3)) → BatchNorm → MaxPool
Conv2D(64, (3, 3)) → BatchNorm → MaxPool
Conv2D(128, (3, 3)) → BatchNorm → MaxPool
```
- **Progressive Feature Extraction**: Filter count increases (32→64→128) to capture complex patterns in later layers.
- **Max-Pooling**: Reduces spatial dimensions efficiently without losing key features.
- **Batch Normalization**: Promotes stable learning by normalizing activations.

### 2. Regularization Techniques
- **Batch Normalization**: Applied after each convolutional layer to stabilize learning.
- **Dropout (0.5)**: Added in dense layers to prevent overfitting.

### 3. Dense Layers
- **128 units** followed by **10-unit softmax** for final classification. This layer choice provides enough capacity to learn meaningful representations while remaining efficient.

---

## Key Performance Factors

- **Native Resolution** (32x32): Avoids resizing issues, maintains training efficiency, and preserves CIFAR-10 image features.
- **Data Augmentation**: Improves model robustness by introducing controlled variations in the data.
- **Balanced Architecture**: Carefully chosen model depth and regularization keep the parameter count manageable while achieving strong results.

---

## Validation Results
- Achieved **72% accuracy** at the native 32x32 resolution, outperforming trials with larger resolutions.

---

## Recommendations for Further Improvements
- **Learning Rate Scheduling**: Could improve training convergence.
- **Additional Regularization**: Potentially beneficial if signs of overfitting appear.
- **Skip Connections**: Useful for enhancing gradient flow in deeper networks.
- **Extended Data Augmentation**: Brightness, contrast adjustments, zoom variations, and random cropping could add further resilience to variations in the data.

---



Choosing **32x32** as the model resolution, rather than higher resolutions like **128x128**, was key to balancing **accuracy** and **efficiency**. Larger resolutions provided no significant accuracy benefit while adding computational cost and potentially introducing artifacts. By aligning with the CIFAR-10 native resolution, this model achieves optimal feature representation with minimal processing overhead.
