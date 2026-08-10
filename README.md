# 🌾 Crop & Fertilizer Recommendation System for Amravati, Maharashtra

An **Agricultural Machine Learning Recommendation System** that recommends a suitable **crop and fertilizer** based on regional soil and environmental conditions.

The project is specifically designed around agricultural conditions in **Amravati district, Maharashtra**, covering **Amravati, Morshi, Warud, and Chandur Bazar**.

---

## 📌 Project Overview

Choosing the right crop and fertilizer depends heavily on soil characteristics, nutrient availability, rainfall, temperature, and geographical conditions.

This project uses **Machine Learning** to analyze these parameters and recommend:

* 🌱 Suitable Crop
* 🧪 Recommended Fertilizer

The system allows users to select their **Taluka and soil type**, followed by soil nutrient and environmental parameters. A **Random Forest Classifier** then predicts the most suitable crop, and the corresponding fertilizer recommendation is obtained from the agricultural dataset.

---

## 🎯 Objectives

* Develop a region-specific crop recommendation system.
* Use soil and environmental parameters for data-driven recommendations.
* Recommend suitable fertilizers for the predicted crop.
* Focus on agricultural conditions of Amravati district.
* Provide an interactive interface using Jupyter/Google Colab widgets.
* Demonstrate the application of Machine Learning in precision agriculture.

---

## 🗺️ Geographic Coverage

The dataset currently covers four Talukas:

| Taluka        |
| ------------- |
| Amravati      |
| Morshi        |
| Warud         |
| Chandur Bazar |

These locations are used as geographical context for the crop recommendation process.

---

## 📊 Dataset

The project uses a custom dataset:

**`FinalAmravati Crop and fertilizer dataset.csv`**

The dataset contains **4,513 records and 10 features**.

### Dataset Features

| Feature       | Description           |
| ------------- | --------------------- |
| `Taluka_Name` | Taluka/region         |
| `Soil_color`  | Soil color/type       |
| `Nitrogen`    | Nitrogen content      |
| `Phosphorus`  | Phosphorus content    |
| `Potassium`   | Potassium content     |
| `pH`          | Soil pH value         |
| `Rainfall`    | Rainfall condition    |
| `Temperature` | Temperature condition |
| `Crop`        | Target crop           |
| `Fertilizer`  | Associated fertilizer |

The dataset contains no missing values and no duplicate rows.

### Soil Types

The dataset includes soil categories such as:

* Black
* Red
* Dark Brown
* Light Brown
* Medium Brown
* Reddish Brown

### Supported Crops

The dataset includes crops such as:

* Orange
* Jowar
* Cotton
* Rice
* Wheat
* Groundnut
* Maize
* Tur
* Urad
* Moong
* Gram
* Masoor
* Soybean
* Ginger
* Turmeric
* Chickoo

---

## 🧪 Input Parameters

The model uses the following parameters:

```text
Taluka
Soil Color
Nitrogen
Phosphorus
Potassium
pH
Rainfall
Temperature
```

These parameters represent a combination of **regional, soil, nutrient and environmental information**.

---

## 🤖 Machine Learning Approach

### 1. Data Loading

The dataset is loaded using Pandas.

```python
import pandas as pd

dataset = pd.read_csv(
    "FinalAmravati Crop and fertilizer dataset.csv"
)
```

### 2. Exploratory Data Analysis

The project performs basic data analysis including:

* Dataset shape
* Dataset information
* Missing-value analysis
* Duplicate-value analysis
* Descriptive statistics
* Correlation analysis
* Correlation heatmap

The notebook uses **Matplotlib and Seaborn** for visualization.

---

## 🔄 Data Preprocessing

Categorical variables are converted into numerical representations using **One-Hot Encoding**.

The categorical features are:

```text
Taluka_Name
Soil_color
```

The implementation uses:

```python
OneHotEncoder(handle_unknown='ignore')
```

This allows categorical values to be transformed into a machine-learning-compatible representation.

---

## 🌲 Model

The project uses:

### Random Forest Classifier

```python
RandomForestClassifier(
    n_estimators=100,
    random_state=42
)
```

The dataset is divided into:

```text
80% → Training
20% → Testing
```

using:

```python
train_test_split(
    X_encoded,
    dataset['Crop'],
    test_size=0.2,
    random_state=42
)
```

The Random Forest model learns the relationship between the encoded regional/soil information and the crop labels.

---

## 🧠 Recommendation Pipeline

The complete workflow is:

```text
                 ┌──────────────────────┐
                 │   User Input         │
                 └──────────┬───────────┘
                            │
                            ▼
              ┌─────────────────────────┐
              │      Taluka Selection   │
              └────────────┬────────────┘
                           │
                           ▼
              ┌─────────────────────────┐
              │      Soil Color         │
              └────────────┬────────────┘
                           │
                           ▼
        ┌────────────────────────────────────┐
        │ Soil & Environmental Parameters    │
        │                                    │
        │ Nitrogen                           │
        │ Phosphorus                         │
        │ Potassium                          │
        │ pH                                 │
        │ Rainfall                           │
        │ Temperature                        │
        └─────────────────┬──────────────────┘
                          │
                          ▼
                ┌──────────────────┐
                │ One-Hot Encoding │
                └────────┬─────────┘
                         │
                         ▼
              ┌──────────────────────┐
              │ Random Forest Model  │
              └──────────┬───────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Crop Prediction │
                └────────┬────────┘
                         │
                         ▼
             ┌───────────────────────┐
             │ Fertilizer Mapping    │
             └───────────┬───────────┘
                         │
                         ▼
             ┌────────────────────────┐
             │ Final Recommendation   │
             │                        │
             │ 🌱 Crop                │
             │ 🧪 Fertilizer          │
             └────────────────────────┘
```

---

## 🖥️ Interactive Interface

The notebook uses **`ipywidgets`** to create an interactive recommendation interface.

Users can select:

* Taluka
* Soil Color
* Nitrogen
* Phosphorus
* Potassium
* pH
* Rainfall
* Temperature

The available values are dynamically updated based on the selected **Taluka and Soil Color**.

The final interface provides a button:

```text
Recommend Crop and Fertilizer
```

and displays:

```text
Recommended Crop: <crop>

Recommended Fertilizer: <fertilizer>
```

---

## 🧪 Example

For a given combination of:

```text
Taluka      → Amravati
Soil Color  → Black
Nitrogen    → 75
Phosphorus  → 50
Potassium   → 100
pH          → 6.5
Rainfall    → 1000
Temperature → 20
```

the system processes the input through the encoding and Random Forest model and produces a crop recommendation followed by its associated fertilizer recommendation.

---

## 🛠️ Tech Stack

### Programming Language

* Python

### Machine Learning

* Scikit-Learn
* Random Forest Classifier
* One-Hot Encoding
* Train/Test Split

### Data Processing

* Pandas
* NumPy

### Visualization

* Matplotlib
* Seaborn

### Interactive UI

* ipywidgets
* Jupyter Notebook
* Google Colab

---

## 📁 Repository Structure

```text
Crop-and-fertilizer-Recommend-model-for-Amravati-MH-
│
├── Crop_and_fertilizer_Recommend_model_for_Amravati_Areaa.ipynb
│
├── Crop_and_fertilizer_Recommend_model_for_Amravati_Areaa (1).ipynb
│
├── FinalAmravati Crop and fertilizer dataset.csv
│
├── Flask.png
│
├── Hotmap.png
│
├── sample output.png
│
└── README.md
```

The repository currently contains two notebook versions along with the dataset and visualization/output images.

---

## 🚀 How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/VedantDgit/Crop-and-fertilizer-Recommend-model-for-Amravati-MH-.git
```

### 2. Navigate to the Project

```bash
cd Crop-and-fertilizer-Recommend-model-for-Amravati-MH-
```

### 3. Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scikit-learn ipywidgets
```

### 4. Open the Notebook

```bash
jupyter notebook
```

or open the notebook using **Google Colab**.

### 5. Run the Notebook

Open:

```text
Crop_and_fertilizer_Recommend_model_for_Amravati_Areaa.ipynb
```

Run the cells sequentially and interact with the recommendation widgets.

---

## 📈 Exploratory Analysis

The project includes correlation analysis of numerical agricultural parameters.

A correlation matrix is generated using:

```python
numeric_dataset = dataset.select_dtypes(
    include=['number']
)

corr = numeric_dataset.corr()
```

A heatmap is then generated using Seaborn to visualize relationships between numerical variables.

---

## 💡 Key Highlights

* 🌾 Region-specific agricultural recommendation
* 🗺️ Supports multiple Talukas of Amravati district
* 🧪 Uses soil nutrient information
* 🌦️ Uses rainfall and temperature
* 🤖 Random Forest based crop prediction
* 🧬 One-Hot Encoding for categorical variables
* 🖥️ Interactive Jupyter interface
* 🌱 Crop + fertilizer recommendation
* 📊 Exploratory data analysis and correlation visualization
* 📚 Custom regional agricultural dataset

---

## 🔮 Future Improvements

The current project can be extended into a production-ready agricultural AI platform.

### Possible improvements:

* Deploy the model using Flask/FastAPI
* Create a React-based web interface
* Add real-time weather API integration
* Add soil-test data integration
* Add crop yield prediction
* Add fertilizer quantity prediction
* Add fertilizer dosage recommendations
* Add crop disease detection using Deep Learning
* Add explainable AI using SHAP
* Compare Random Forest with XGBoost, Gradient Boosting and other algorithms
* Add model evaluation metrics such as Accuracy, Precision, Recall and F1-score
* Add model serialization using Joblib
* Deploy the application on AWS/Render

---

## ⚠️ Disclaimer

This project is intended for **educational and research purposes**.

The recommendations generated by the model should not be treated as a substitute for professional agricultural advice, laboratory soil testing, or guidance from agricultural experts.

---

## 👨‍💻 Author

**Vedant Deshmukh**

B.Tech – Computer Science Engineering
Artificial Intelligence & Machine Learning

### GitHub

https://github.com/VedantDgit

---

## ⭐ If you find this project useful

Consider giving the repository a ⭐ on GitHub!

---

## 📜 License

This project is available for educational and research purposes.

