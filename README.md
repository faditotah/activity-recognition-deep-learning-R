# Assignment 2: Human Activity Recognition Using Deep Learning Models

---

## Exercise 1

### Question 1: CNN Architecture Overview

- **Input images:** Colored, 256 x 256 pixels, 3 channels (W x H x D)  
- **Convolutional layers:** 3 layers  
- **Filter sizes:**  
  - 1st layer: 6x6  
  - 2nd layer: 4x4  
  - 3rd layer: 2x2  
- **Batches per epoch:** 185  
- **Activations:** ReLU (hidden layers), SoftMax (output)  
- **Regularization:** L2 regularization applied in dense_1 layer  

### Question 2: Parameter Calculations

- **Second convolutional layer parameters:**  
  - Depth after conv_1: 64  
  - Filter size per filter: 4 × 4 × 64 + 1 bias = 1025  
  - Number of filters: 128  
  - **Total parameters:** 128 × 1025 = 131,200  

- **First dense layer parameters:**  
  - Layer 3 size: (2 × 2 × 128 + 1) × 128 = 65,664  
  - Dense layer params: (65,664 + 1) × 64 = 4,202,560  

---

## Exercise 2.1: Activity Recognition Models

### Dataset and Setup

- **Data:** `"data_assignment_2_activity_recognition.RData"`  
- **Subjects:** 8 people (4M, 4F) performing 19 activities  
- **Sensors:** 5 units/person, each with 9 sensors → 45 sensors total  
- **Sampling:** 25 Hz, segmented into 5-second windows (125 time points)  
- **Segment shape:** 125 × 45 matrix, flattened to 5625 features  
- **Training/Validation:** 8,170 segments (430 per activity)  
- **Test:** 950 segments (50 per activity)  

---

### Models Implemented

#### Model 1: Convolutional Neural Network (CNN)

- Three convolutional layers with increasing filters (32 → 64)  
- Kernel sizes: (2x2), (3x3), (3x3)  
- Max-pooling layers (2x2)  
- Dense layer with 64 units + ReLU  
- Dropout (10%)  
- L2 regularization (λ = 0.1)  

#### Model 2: Deep Neural Network (DNN)

- Five fully connected layers with decreasing neurons (1024 → 128)  
- Batch normalization and dropout layers (gradually decreasing dropout rates)  
- L2 regularization (λ = 0.001)  

#### Model 3: LSTM Recurrent Neural Network (RNN)

- Two LSTM layers (64 units, then 32 units)  
- Dense output layer with softmax  
- Designed to capture temporal dependencies  

---

### Common Features Across Models

- Data normalized by max value to [-1, 1]  
- Adam optimizer used for training  
- Batch size ~10% of training set (~700)  

---

### Training Summary

- All models trained for 75 epochs  
- Validation performed on held-out 950 samples  

---

## Model Comparisons

- Accuracy and loss plotted for training and validation sets  
- CNN showed stable training and high accuracy (~93% train, ~95% val)  
- DNN showed high training accuracy (~96%) but slight overfitting (~92% val)  
- LSTM had unstable training and lower accuracy (~53% train and val)  

**Conclusion:** CNN is the best performing model balancing accuracy, stability, and generalization.

---

## Exercise 2.2: CNN Model Evaluation on Test Data

- Test accuracy: **69%**  
- Test loss: **1.22**  
- Strong performance on activities like horizontal cycling, elevator movement, jumping, and lying on the right side  
- Struggles with sitting, stair descent, standing, treadmill walking, and stepper activities  
- Notable misclassifications observed, indicating room for improvement  

---

## Usage Instructions

1. Load dataset and required libraries (`keras3`, `tfruns`)  
2. Normalize and reshape data for each model  
3. Train selected model (CNN recommended) for 75 epochs  
4. Evaluate using accuracy and confusion matrices  
5. Visualize training performance with provided plots  

---

## Requirements

- R (version compatible with keras3)  
- Packages: `keras3`, `tfruns`  

---

## Notes

- CNN model outperforms DNN and LSTM in this task  
- Data imbalance and similar activity patterns affect accuracy  
- Further tuning and data augmentation could improve results  

---

If you want, I can help format the code chunks or add images of plots next! Just let me know 💻✨
