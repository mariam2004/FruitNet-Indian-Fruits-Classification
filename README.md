# FruitNet - Indian Fruits Classification

A deep learning project for classifying Indian fruits based on two tasks:

- Fruit Type Classification
- Fruit Quality Classification

The project uses a Multi-Task Convolutional Neural Network (CNN) trained on the **FruitNet: Indian Fruits Dataset with Quality**.

---

## Project Overview

The goal of this project is to build a single deep learning model that performs two classification tasks simultaneously from the same fruit image.

Given an input image, the model predicts:

1. The type of fruit.
2. The quality of the fruit.

This is implemented using a **Multi-Task Learning** architecture with two output layers.

---

## Dataset

The project uses the:

**FruitNet: Indian Fruits Dataset with Quality**

The dataset contains fruit images organized by quality and fruit type.

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

The dataset is **not included** in this repository because of its large size.

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

Each image is processed using the following steps:

1. Convert BGR images to RGB.
2. Resize images to `128 × 128`.
3. Normalize pixel values to the range `[0, 1]`.
4. Encode quality labels using `LabelEncoder`.
5. Encode fruit labels using `LabelEncoder`.
6. Convert labels to one-hot encoded vectors.

---

## Model Architecture

The project uses a **Multi-Task Convolutional Neural Network (CNN)**.

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
Softmax              Softmax
```

### Quality Classification

The first output predicts the **quality category** of the fruit.

### Fruit Classification

The second output predicts the **fruit type**.

---

## Training

The model uses:

- **Optimizer:** Adam
- **Loss Function:** Categorical Crossentropy
- **Metric:** Accuracy
- **Dropout:** 0.5
- **Early Stopping:** Used to reduce overfitting

The model is trained using both outputs simultaneously.

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

## Evaluation

The model is evaluated using several metrics and visualization techniques.

### Classification Reports

Separate classification reports are generated for:

- Fruit Quality
- Fruit Type

The reports include:

- Precision
- Recall
- F1-score
- Accuracy

### Confusion Matrices

Confusion matrices are generated for:

- Quality Classification
- Fruit Classification

### Training Curves

The project visualizes:

- Training and validation loss
- Training and validation accuracy

These visualizations help analyze model performance and identify potential overfitting.

---

## Model Prediction

The trained model can predict both outputs from a single fruit image.

```text
Input Image
     │
     ├──► Fruit Type Prediction
     │
     └──► Fruit Quality Prediction
```

### Example

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

---

## Installation

### Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/FruitNet-Indian-Fruits-Classification.git
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
6. Train the model.
7. Evaluate the model.
8. Generate predictions.

---

## Model File

The trained model is stored in:

```text
models/fruit_quality_model.h5
```

The model contains the trained **Multi-Task CNN** used for fruit type and fruit quality classification.

---

## Future Improvements

- Transfer learning using pretrained CNN architectures.
- Data augmentation.
- Hyperparameter tuning.
- More robust train/validation/test splitting.
- Model deployment using Streamlit.
- Web-based fruit classification application.

---
