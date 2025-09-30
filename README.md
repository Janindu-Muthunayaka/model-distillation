# model-distillation
**Classification**

# Dataset
Uses the **MNIST dataset** for a classification task. MNIST consists of 70,000 grayscale images of handwritten digits (0-9), each sized 28x28 pixels. These are flattened into 784-dimensional vectors and normalized to the range [0, 1]. 
The dataset is ALREADY split into 60,000 training samples and 10,000 test samples, making it more complex than the Wine dataset (used in v1) to better highlight performance differences in knowledge distillation.

# Models
- **Teacher Model**: A large multi-layer perceptron (MLP) with the following architecture:
  - Input: 784 (flattened image)
  - Hidden layers: 1024 → 512 → 256 → 128 → 64 (all with ReLU activation)
  - Output: 10 (for digit classes)
  - This is significantly larger, with more parameters, leading to higher accuracy but slower inference.

- **Student Model**: A smaller MLP trained via knowledge distillation from the Teacher.
  - Input: 784
  - Hidden layers: 128 → 64 (with ReLU)
  - Output: 10
  - It benefits from the Teacher's "soft targets" for better accuracy than direct training.

- **Person Model**: Identical architecture to the Student but trained directly on the dataset (no distillation).
  - Used as a baseline to compare against the distilled Student.

# Epochs
The training runs for **20 epochs** across all models. This is reduced from the original 50 to keep training efficient while allowing convergence and visible differences in accuracy and loss. Progress is printed every 5 epochs for cleanliness.

**Regression**

# Dataset
The code uses the **California Housing dataset** for a regression task. This dataset contains 20,640 samples with 8 numerical features each, representing different housing attributes (e.g., median income, average rooms, population). The target is the median house value. Features are standardized to zero mean and unit variance, and the data is split into 80% training and 20% testing sets. This dataset is more complex than simpler regression datasets to highlight the effects of knowledge distillation.

# Models

**Teacher Model**: A large fully connected neural network with the following architecture:
Input: 8 (features)
Hidden layers: 512 → 256 → 128 → 64 → 32 (all with ReLU activation)
Output: 1 (median house value)
This model has many parameters, leading to high accuracy but slower inference.

**Student Model**: A smaller neural network trained via knowledge distillation from the Teacher.
Input: 8
Hidden layers: 16 → 8 (with ReLU)
Output: 1
It uses a combination of hard loss (true labels) and soft loss (Teacher outputs) to improve performance over direct training.
**Person Model**: Identical architecture to the Student but trained directly on the dataset without distillation.
Input: 8
Hidden layers: 16 → 8 (with ReLU)
Output: 1
Used as a baseline to compare against the distilled Student.

# Epochs
All models are trained for 100 epochs to allow the Teacher to exaggerate performance differences. Loss progress is printed every 10 epochs for clarity. The same number of epochs is applied to the Student and Person models to maintain a fair comparison.
