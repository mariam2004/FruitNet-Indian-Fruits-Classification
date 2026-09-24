# FruitNet - Indian Fruits Classification

A deep learning project for **fruit type and fruit quality classification** using a Multi-Task Convolutional Neural Network (CNN).

The model is trained on the **FruitNet: Indian Fruits Dataset with Quality** and performs two classification tasks simultaneously from a single fruit image:

- **Fruit Type Classification**
- **Fruit Quality Classification**

---

## Project Overview

The goal of this project is to develop a single deep learning model capable of predicting both the **fruit class** and its **quality category** from the same input image.

The project uses a **Multi-Task Learning** architecture with:

- A shared CNN feature extraction backbone.
- A dedicated output layer for fruit quality.
- A dedicated output layer for fruit classification.

This approach allows the model to learn shared visual features while solving both classification tasks simultaneously.

---

## Dataset

The project uses the:

**FruitNet: Indian Fruits Dataset with Quality**

The dataset contains fruit images organized according to fruit type and quality.

### Dataset Structure

```text
Processed Images_Fruits/
│
├── Bad Quality_Fruits/
│   ├── Apple/
│   ├── Banana/
│   └── ...
│
├── Good Quality_Fruits/
│   ├── Apple/
│   ├── Banana/
│   └── ...
│
└── Mixed Quality_Fruits/
    ├── Apple/
    ├── Banana/
    └── ...
```

### Dataset Statistics

- **Total Images:** 19,526
- **Image Size:** 128 × 128 × 3
- **Quality Classes:** 3
- **Fruit Classes:** 18

The dataset is **not included in this repository** because of its large size.

---

## Technologies Used

- Python
- NumPy
- OpenCV
- Matplotlib
- Seaborn
- Scikit-learn
- TensorFlow
- Keras
- Jupyter Notebook

---

## Image Preprocessing

Each image goes through the following preprocessing pipeline:

1. Convert images from BGR to RGB.
2. Resize images to `128 × 128`.
3. Normalize pixel values to `[0, 1]`.
4. Encode quality labels using `LabelEncoder`.
5. Encode fruit labels using `LabelEncoder`.
6. Convert labels into one-hot encoded vectors.

---

## Model Architecture

The project uses a **Multi-Task Convolutional Neural Network (CNN)** with shared feature extraction and two classification outputs.

```text
Input Image
128 × 128 × 3
       │
       ▼
Conv2D (32)
       │
MaxPooling
       │
Conv2D (64)
       │
MaxPooling
       │
Conv2D (128)
       │
MaxPooling
       │
Flatten
       │
Dense (256)
       │
Dropout (0.5)
       │
       ├──────────────────┐
       ▼                  ▼
Quality Output       Fruit Output
3 Classes            18 Classes
Softmax              Softmax
```

### Model Configuration

- **Input:** `128 × 128 × 3`
- **Convolutional Layers:** 3
- **Dense Layer:** 256 units
- **Dropout:** 0.5
- **Quality Output:** 3 classes
- **Fruit Output:** 18 classes
- **Total Parameters:** 6,521,429
- **Trainable Parameters:** 6,521,429

---

## Training

The model was trained using:

| Configuration | Value |
|---|---|
| Optimizer | Adam |
| Loss Function | Categorical Crossentropy |
| Metric | Accuracy |
| Dropout | 0.5 |
| Batch Size | 32 |
| Maximum Epochs | 50 |
| Early Stopping | Enabled |

Early Stopping was applied by monitoring validation loss and restoring the best model weights.

The model was trained using both outputs simultaneously:

```python
model.compile(
    optimizer="adam",
    loss={
        "quality_output": "categorical_crossentropy",
        "fruit_output": "categorical_crossentropy"
    },
    metrics={
        "quality_output": "accuracy",
        "fruit_output": "accuracy"
    }
)
```

---

## Model Performance

The model achieved strong validation performance on both classification tasks.

| Task | Validation Accuracy |
|---|---:|
| Fruit Quality Classification | **98%** |
| Fruit Classification | **96%** |

### Quality Classification

The quality classification achieved:

- **Accuracy:** 98%
- **Weighted F1-score:** 0.98

Performance by class:

| Class | Precision | Recall | F1-score |
|---|---:|---:|---:|
| Bad Quality | 0.98 | 0.98 | 0.98 |
| Good Quality | 0.99 | 0.98 | 0.99 |
| Mixed Quality | 0.86 | 0.93 | 0.90 |

### Fruit Classification

The fruit classification achieved:

- **Accuracy:** 96%
- **Weighted F1-score:** 0.96
- **Macro F1-score:** 0.93

The model was evaluated across all **18 fruit classes** using precision, recall, and F1-score.

---

## Evaluation

Several evaluation methods were used to analyze model performance.

### Classification Reports

Separate classification reports were generated for:

- Fruit Quality Classification
- Fruit Classification

The reports include:

- Precision
- Recall
- F1-score
- Accuracy

### Confusion Matrices

Confusion matrices were generated for both:

- Quality Classification
- Fruit Classification

They provide a detailed view of correct predictions and class-level misclassifications.

### Training Curves

The training history was visualized using:

- Training vs. validation loss
- Training vs. validation accuracy

These plots help analyze model convergence and identify potential overfitting.

---

## Prediction

The trained Multi-Task CNN produces two predictions from a single fruit image:

```text
                 Input Image
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
   Fruit Type Prediction   Quality Prediction
          │                     │
       Apple              Good Quality
```

Example:

```text
Actual:
Apple | Good Quality_Fruits

Predicted:
Apple | Good Quality_Fruits
```

---

## Project Structure

```text
FruitNet-Indian-Fruits-Classification/
│
├── README.md
├── requirements.txt
├── .gitignore
│
└── FruitNet_Multitask_CNN.ipynb
```

> The dataset and trained model are not included in the repository.

---

## Installation

### Clone the Repository

```bash
git clone https://github.com/mariam2004/FruitNet-Indian-Fruits-Classification.git
cd FruitNet-Indian-Fruits-Classification
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Running the Project

The project was developed using **Kaggle Notebooks**.

To reproduce the project:

1. Download the FruitNet dataset.
2. Open `FruitNet_Multitask_CNN.ipynb`.
3. Add the dataset to your Kaggle environment.
4. Update the dataset path if necessary.
5. Run the notebook cells in order.
6. Train the Multi-Task CNN.
7. Evaluate the model using classification reports and confusion matrices.
8. Generate fruit type and quality predictions.

---

## Repository Contents

This repository contains:

- `FruitNet_Multitask_CNN.ipynb` — Complete data preprocessing, model training, evaluation, and prediction pipeline.
- `requirements.txt` — Required Python dependencies.
- `README.md` — Project documentation.
- `.gitignore` — Files and directories excluded from version control.

The **dataset and trained model weights are excluded** because of their size.

---

## Future Improvements

- Transfer learning using pretrained CNN architectures.
- Data augmentation to improve generalization.
- Hyperparameter tuning.
- A dedicated train/validation/test split.
- Model optimization and lightweight deployment.
- Streamlit-based web application.
- Real-time fruit image classification.

---

GitHub:  
https://github.com/mariam2004

LinkedIn:  
https://linkedin.com/in/mariam-kedr-mariamahmed/
