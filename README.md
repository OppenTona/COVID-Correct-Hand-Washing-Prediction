# COVID-19 Correct Hand Washing Prediction

A machine learning project that uses computer vision to predict correct hand washing techniques during the COVID-19 pandemic. This project implements MobileNet architecture for image classification to identify proper hand washing practices.

## 📋 Project Overview

This repository contains coursework for CHS2406 - Data-driven Artificial Intelligence course at the University of Huddersfield. The project focuses on developing an AI model to automatically classify hand washing images and determine if proper hand washing techniques are being followed.

## 🎯 Objectives

- Develop a deep learning model for hand washing technique classification
- Implement MobileNet architecture for efficient mobile deployment
- Analyze and clean image labeling data
- Evaluate model performance for real-world application

## 📁 Repository Structure

```
COVID-Correct-Hand-Washing-Prediction/
├── CHS2406_Coursework2_Data_Repository/    # Dataset directory
├── u2560895_NguyenTheToan_Asignment2_MoblieNET.ipynb    # Main MobileNet implementation
├── labelling_error.ipynb                   # Data cleaning and error analysis
├── image_labels.txt                        # Original image labels
├── image_labels.cleaned.txt               # Cleaned image labels
├── assignment2_rubrics.pdf                # Assignment requirements and rubrics
└── README.md                              # This file
```

## 🚀 Getting Started

### Prerequisites

- Python 3.7+
- Jupyter Notebook
- TensorFlow/Keras
- NumPy
- Pandas
- Matplotlib
- OpenCV

### Installation

1. Clone the repository:
```bash
git clone https://github.com/OppenTona/COVID-Correct-Hand-Washing-Prediction.git
cd COVID-Correct-Hand-Washing-Prediction
```

2. Install required dependencies:
```bash
pip install tensorflow numpy pandas matplotlib opencv-python jupyter
```

3. Launch Jupyter Notebook:
```bash
jupyter notebook
```

## 📊 Dataset

The project uses a custom dataset of hand washing images with the following structure:
- **Image Labels**: Contains annotations for correct/incorrect hand washing techniques
- **Cleaned Labels**: Processed version with error corrections and data validation
- **Data Repository**: Directory containing the actual image dataset

### Data Preprocessing

The `labelling_error.ipynb` notebook handles:
- Detection and correction of labeling errors
- Data validation and cleaning
- Statistical analysis of the dataset

## 🧠 Model Architecture

### MobileNet Implementation

The main model (`u2560895_NguyenTheToan_Asignment2_MoblieNET.ipynb`) features:
- **Base Architecture**: MobileNet for efficient computation
- **Transfer Learning**: Pre-trained weights for faster convergence
- **Custom Classification Head**: Tailored for hand washing classification
- **Mobile Optimization**: Designed for deployment on mobile devices

### Key Features:
- Lightweight architecture suitable for mobile deployment
- High accuracy in hand washing technique classification
- Real-time inference capabilities
- Robust performance across different lighting conditions

## 📈 Results

The model demonstrates:
- Effective classification of correct vs incorrect hand washing techniques
- Optimized performance for mobile device deployment
- Comprehensive evaluation metrics and validation

## 🔧 Usage

1. **Data Preparation**: Run `labelling_error.ipynb` to clean and prepare the dataset
2. **Model Training**: Execute `u2560895_NguyenTheToan_Asignment2_MoblieNET.ipynb` to train the MobileNet model
3. **Evaluation**: Analyze model performance using the built-in evaluation metrics

## 📝 Course Information

- **Course**: CHS2406 - Data-driven Artificial Intelligence
- **Institution**: University of Huddersfield
- **Assignment**: Coursework 2 - Image Classification
- **Student ID**: u2560895
- **Student Name**: Nguyen The Toan

## 🤝 Contributing

This is a coursework project. For educational purposes, please refer to the assignment rubrics and guidelines provided in `assignment2_rubrics.pdf`.

## 📄 License

This project is created for educational purposes as part of university coursework.

## 📧 Contact

For questions or collaboration:
- GitHub: [@OppenTona](https://github.com/OppenTona)
- Project Link: [COVID-Correct-Hand-Washing-Prediction](https://github.com/OppenTona/COVID-Correct-Hand-Washing-Prediction)

---

**Note**: This project was developed during the COVID-19 pandemic to contribute to public health awareness and proper hygiene practices through AI technology.
