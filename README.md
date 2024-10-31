# CIFAR-10 CNN Classifier

This repository contains an implementation of a Convolutional Neural Network (CNN) for multi-class image classification on the CIFAR-10 dataset.

## Data Preprocessing Pipeline

### 1. Image Size Selection
- **Resolution**: 32x32 (native CIFAR-10 size)
- **Benefits**:
  - Achieves optimal accuracy (72%) compared to larger resolutions
  - Maintains efficient computational requirements
  - Avoids interpolation artifacts for better feature preservation

### 2. Data Augmentation Techniques
Using TensorFlow’s `ImageDataGenerator`, the following augmentations were applied:
- **Rotation** (15 degrees): Handles slight orientation variations
- **Width/Height Shifts** (10%): Improves position invariance
- **Horizontal Flip**: Doubles effective dataset size and combats overfitting

### 3. Normalization
- **Method**: Pixel values scaled to [0,1] by dividing by 255.0.
- **Importance**: Stabilizes training, improves gradient flow, and enhances model convergence.

### 4. Image Integrity Checks
- Ensures data quality through image corruption detection before training.

## Model Architecture

1. **Convolutional Layers**:
   - Three layers with progressively increasing filters (32→64→128)
   - Uses batch normalization and max-pooling for effective feature extraction and spatial dimension reduction

2. **Regularization Techniques**:
   - Batch Normalization after each convolutional layer
   - Dropout (0.5) in dense layers to mitigate overfitting

3. **Dense Layers**:
   - 128 units followed by a 10-unit softmax layer, suited for 10-class classification

## Key Performance Factors
- **Native Resolution**: Optimal performance at 32x32, avoiding artifacts and maintaining training efficiency.
- **Augmentation Impact**: Generalizes the model, making it robust to slight variations in the dataset.
- **Architecture Efficiency**: Balances depth, parameter count, and regularization to achieve strong results.

## Validation Results
- Achieved 72% accuracy with this architecture, outperforming larger input sizes.

## Potential Improvements
- **Learning Rate Scheduling** for smoother convergence
- **Additional Regularization** techniques if needed
- **Skip Connections** for enhanced gradient flow
- **Extended Augmentation**: Brightness, contrast, zoom variations, and random cropping for added robustness.

## Getting Started

To run this model, clone the repository and install the required dependencies.

```bash
git clone https://github.com/your_username/CIFAR-10_CNN_Classifier.git
cd CIFAR-10_CNN_Classifier
pip install -r requirements.txt
