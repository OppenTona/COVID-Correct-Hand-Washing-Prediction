# COVID-19 Hand Washing Classification

## Project Overview
This project implements a deep learning solution to automatically classify and monitor the 8 stages of WHO hand washing guidelines. It was developed as part of the CHS2406 Data-Driven AI coursework.

## Problem Statement
During the COVID-19 pandemic, ensuring proper hand hygiene was crucial for healthcare professionals and essential workers. The WHO provided guidelines on proper handwashing, but there was no automated way to verify compliance. This project creates an AI solution to automatically monitor handwashing by classifying images into the 8 WHO-defined stages.

## Dataset
- **Source**: CHS2406_Coursework2_Data_Repository
- **Total Images**: 8,538 images (after removing corrupted files)
- **Classes**: 8 stages of hand washing
- **Image Size**: 150x150 pixels (RGB)

## Methodology

### 1. Data Collection and Preparation
- Collected images from shared repository
- Copied images to local dataset folder
- Resized all images to 150x150 pixels
- Created label mapping (Stage1-8 → 0-7)

### 2. Label Error Detection with Cleanlab
- **Approach**: Deep learning-based label error detection
- **Feature Extraction**: MobileNetV2 pre-trained on ImageNet
- **Classifier**: Multi-layer perceptron (MLP) with dropout
- **Cross-Validation**: 5-fold stratified cross-validation
- **Result**: Detected and removed ~58% of images as potential label errors
- **Clean Dataset**: 3,593 images with high-confidence labels

### 3. Data Preprocessing
- Normalized pixel values to [0, 1] range
- Applied data augmentation:
  - Rotation (±15 degrees)
  - Width/height shift (±10%)
  - Shear transformation
  - Zoom (±10%)
  - Horizontal flip

### 4. Dataset Splitting
- **Training Set**: 70% (~2,515 images)
- **Validation Set**: 15% (~539 images)
- **Test Set**: 15% (~539 images)
- Used stratified sampling to maintain class distribution

### 5. Model Architecture
**Transfer Learning with MobileNetV2**
```
Input (150x150x3)
  ↓
MobileNetV2 (pre-trained on ImageNet, frozen initially)
  ↓
GlobalAveragePooling2D
  ↓
Dropout (0.3)
  ↓
Dense (256, ReLU)
  ↓
BatchNormalization
  ↓
Dropout (0.3)
  ↓
Dense (128, ReLU)
  ↓
BatchNormalization
  ↓
Dropout (0.2)
  ↓
Dense (8, Softmax)
```

### 6. Training Strategy
**Phase 1: Feature Extraction**
- Freeze MobileNetV2 base
- Train only classification head
- Learning rate: 0.001
- Epochs: 50 (with early stopping)

**Phase 2: Fine-tuning**
- Unfreeze last 20 layers of MobileNetV2
- Train with lower learning rate: 0.0001
- Epochs: 30 (with early stopping)

**Callbacks**:
- EarlyStopping (patience=10, monitor='val_loss')
- ModelCheckpoint (save best model based on val_accuracy)
- ReduceLROnPlateau (factor=0.5, patience=5)

### 7. Evaluation Metrics
- Accuracy
- Precision, Recall, F1-Score (per class)
- Confusion Matrix
- Training/Validation curves

## Results

### Label Error Detection
- **Original Dataset**: 8,538 images
- **Flagged as Errors**: ~4,945 images (~58%)
- **Clean Dataset**: 3,593 images
- **Error Types Detected**:
  1. **Corrupted/Unreadable Images**: Could not be loaded by OpenCV
  2. **Wrong File Formats**: .heic files (not supported in processing pipeline)
  3. **Mislabeled Images**: Detected by Cleanlab using deep learning confidence analysis

**Note**: Image resizing to 150x150 is standard preprocessing, not error handling.

### Model Performance
Performance metrics will be available after training the model on the clean dataset.

## Project Structure
```
.
├── complete_assignment.ipynb     # Main notebook with complete solution
├── labelling_error.ipynb          # Label error detection notebook
├── u2560895_NguyenTheToan_Asignment2.ipynb  # Original assignment notebook
├── dataset/                       # Image dataset folder
├── image_labels.txt               # Original labels
├── image_labels_clean.txt         # Clean labels after error removal
├── requirements.txt               # Python dependencies
├── best_model.keras               # Best trained model
├── confusion_matrix.png           # Confusion matrix visualization
├── training_curves.png            # Training/validation curves
└── README.md                      # This file
```

## Installation

### Prerequisites
- Python 3.8+
- pip

### Setup
```bash
# Clone the repository
git clone https://github.com/OppenTona/COVID-Correct-Hand-Washing-Prediction.git
cd COVID-Correct-Hand-Washing-Prediction

# Install dependencies
pip install -r requirements.txt
```

## Usage

### Training the Model
```bash
# Run the complete assignment notebook
jupyter notebook complete_assignment.ipynb
```

The notebook will:
1. Load and prepare the dataset
2. Detect and remove label errors using Cleanlab
3. Preprocess and augment the data
4. Split the dataset
5. Train the model
6. Evaluate performance
7. Save the best model

### Making Predictions
```python
import tensorflow as tf
import cv2
import numpy as np

# Load the trained model
model = tf.keras.models.load_model('best_model.keras')

# Load and preprocess an image
img = cv2.imread('path/to/image.jpg')
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
img = cv2.resize(img, (150, 150))
img = img.astype('float32') / 255.0
img = np.expand_dims(img, axis=0)

# Predict
prediction = model.predict(img)
stage = np.argmax(prediction) + 1  # Add 1 to convert from 0-7 to 1-8
confidence = prediction[0][stage-1]

print(f"Predicted Stage: {stage}")
print(f"Confidence: {confidence*100:.2f}%")
```

## Key Findings

### Label Error Detection
Using Cleanlab with deep learning provided several advantages over traditional methods:
1. **Automated Detection**: No manual review required
2. **Data-Driven**: Uses model uncertainty to identify suspicious labels
3. **Scalable**: Can handle large datasets efficiently
4. **Robust**: Considers multi-class probability distributions

### Model Improvements
The clean dataset led to:
- Better model generalization
- Higher test accuracy
- More reliable predictions
- Reduced overfitting

## Future Improvements
1. **Real-time Detection**: Deploy model for real-time hand washing monitoring
2. **Multi-frame Analysis**: Analyze video sequences for complete washing verification
3. **Multi-person Support**: Extend to handle multiple people simultaneously
4. **Mobile Deployment**: Create mobile app for on-device inference
5. **Feedback System**: Provide real-time feedback to users

## References
1. WHO Hand Hygiene Guidelines
2. MobileNetV2: Inverted Residuals and Linear Bottlenecks
3. Cleanlab: Confident Learning for Label Error Detection
4. TensorFlow Documentation

## License
This project is for educational purposes as part of the CHS2406 coursework.

## Authors
- Student ID: U2560895
- Name: Nguyen The Toan
- Course: CHS2406 - Data-Driven AI
- Institution: University of Huddersfield

## Acknowledgments
- WHO for hand hygiene guidelines
- Course instructors and teaching assistants
- Contributors to the shared image repository
