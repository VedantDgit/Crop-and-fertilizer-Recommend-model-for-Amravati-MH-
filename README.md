# 🌾 Crop and Fertilizer Recommendation System

> **Machine Learning–based crop and fertilizer recommendation system for Amravati district, Maharashtra**

This project is a **Machine Learning-based agricultural recommendation system** that recommends a suitable **crop and fertilizer** based on soil characteristics, nutrient levels, weather conditions, and geographical information.

The system uses a **Random Forest Classifier** to predict the most suitable crop and then recommends an associated fertilizer. It also dynamically generates a **YouTube search link** containing farming and fertilizer-related educational resources for the recommended crop.

---

## 📌 Table of Contents

* [Overview](#-overview)
* [Problem Statement](#-problem-statement)
* [Objectives](#-objectives)
* [Features](#-features)
* [Input Parameters](#-input-parameters)
* [System Workflow](#-system-workflow)
* [Machine Learning Approach](#-machine-learning-approach)
* [YouTube Recommendation](#-youtube-recommendation)
* [Project Structure](#-project-structure)
* [Technology Stack](#-technology-stack)
* [Dataset](#-dataset)
* [Installation](#-installation)
* [Running the Project](#-running-the-project)
* [How the System Works](#-how-the-system-works)
* [Model Evaluation](#-model-evaluation)
* [Example Output](#-example-output)
* [Advantages](#-advantages)
* [Limitations](#-limitations)
* [Future Enhancements](#-future-enhancements)
* [Applications](#-applications)
* [Conclusion](#-conclusion)
* [Author](#-author)

---

# 🌱 Overview

Agricultural productivity depends heavily on selecting an appropriate crop according to the **soil and climatic conditions** of a particular region.

Farmers may have difficulty determining which crop is most suitable for a given combination of:

* Soil type
* Nitrogen availability
* Phosphorus availability
* Potassium availability
* Soil pH
* Rainfall
* Temperature
* Geographical region

This project addresses this problem by using historical agricultural data and a **Random Forest Machine Learning model** to recommend a suitable crop.

After predicting the crop, the system identifies a corresponding fertilizer from the dataset and provides a dynamically generated **YouTube search link** for additional farming information.

---

# ❗ Problem Statement

Farmers need to make decisions regarding crop selection and fertilizer usage based on multiple environmental and soil parameters.

Traditional decision-making can depend heavily on:

* Local knowledge
* Manual soil analysis
* Previous farming experience
* Weather conditions
* Availability of agricultural experts

The objective of this project is to build a data-driven system that can assist in crop selection using Machine Learning.

---

# 🎯 Objectives

The main objectives of this project are:

1. Analyze agricultural data from the Amravati region.
2. Use soil and environmental parameters as Machine Learning features.
3. Predict a suitable crop using Random Forest.
4. Recommend an associated fertilizer.
5. Provide additional farming resources through YouTube.
6. Build an interactive user interface using `ipywidgets`.
7. Create a system that can be extended into a web/mobile agricultural application.

---

# 🚀 Features

### 🌾 Crop Recommendation

Predicts a suitable crop based on the selected agricultural conditions.

### 🧪 Fertilizer Recommendation

Recommends a fertilizer associated with the predicted crop.

### 📍 Taluka-Level Recommendation

The system considers the selected **Taluka** to incorporate geographical information into the prediction.

### 🌱 Soil-Based Filtering

Soil color is dynamically filtered according to the selected Taluka.

### 🧬 NPK Parameters

The model considers:

* Nitrogen
* Phosphorus
* Potassium

### ⚗️ Soil pH

The soil pH value is included as an input feature.

### 🌧️ Rainfall

Rainfall conditions are included in the prediction.

### 🌡️ Temperature

Temperature is considered as an environmental feature.

### 🎥 YouTube Farming Resources

After predicting the crop and fertilizer, the system generates a YouTube search URL such as:

```text
https://www.youtube.com/results?search_query=Wheat+farming+cultivation+fertilizer+Urea
```

This allows users to access additional crop cultivation and fertilizer-related educational videos.

---

# 🧾 Input Parameters

The system accepts the following parameters:

| Parameter     | Description                         |
| ------------- | ----------------------------------- |
| `Taluka_Name` | Selected geographical/taluka region |
| `Soil_color`  | Soil color/type                     |
| `Nitrogen`    | Nitrogen content in soil            |
| `Phosphorus`  | Phosphorus content in soil          |
| `Potassium`   | Potassium content in soil           |
| `pH`          | Soil acidity/alkalinity             |
| `Rainfall`    | Rainfall value                      |
| `Temperature` | Temperature value                   |

### Target Variables

The primary target variable is:

```text
Crop
```

The fertilizer is subsequently retrieved based on the predicted crop.

---

# 🔄 System Workflow

```text
                 ┌──────────────────────┐
                 │      User Input      │
                 └──────────┬───────────┘
                            │
                            ▼
              ┌───────────────────────────┐
              │   Taluka & Soil Color     │
              └─────────────┬─────────────┘
                            │
                            ▼
              ┌───────────────────────────┐
              │ Soil & Weather Parameters │
              │ N, P, K, pH, Rainfall, T  │
              └─────────────┬─────────────┘
                            │
                            ▼
              ┌───────────────────────────┐
              │   Data Preprocessing      │
              └─────────────┬─────────────┘
                            │
                            ▼
              ┌───────────────────────────┐
              │    One-Hot Encoding       │
              │   Categorical Features    │
              └─────────────┬─────────────┘
                            │
                            ▼
              ┌───────────────────────────┐
              │   Random Forest Model     │
              └─────────────┬─────────────┘
                            │
                            ▼
                  ┌──────────────────┐
                  │  Crop Prediction │
                  └────────┬─────────┘
                           │
                           ▼
               ┌────────────────────────┐
               │ Fertilizer Association │
               └───────────┬────────────┘
                           │
                           ▼
              ┌───────────────────────────┐
              │ YouTube Resource Generator│
              └─────────────┬─────────────┘
                            │
                            ▼
              ┌───────────────────────────┐
              │ Final Recommendation      │
              │ Crop + Fertilizer + Video  │
              └───────────────────────────┘
```

---

# 🤖 Machine Learning Approach

## Algorithm: Random Forest Classifier

The project uses a **Random Forest Classifier** for crop classification.

Random Forest is an ensemble learning algorithm that combines multiple decision trees to produce a final prediction.

### Why Random Forest?

Random Forest was selected because:

* It handles nonlinear relationships.
* It works well with mixed feature types.
* It is relatively robust against overfitting.
* It can handle multiple agricultural parameters.
* It generally performs well on tabular datasets.
* It does not require complex feature scaling for tree-based learning.

---

# 🔢 Feature Engineering

The model uses both numerical and categorical features.

### Numerical Features

```text
Nitrogen
Phosphorus
Potassium
pH
Rainfall
Temperature
```

### Categorical Features

```text
Taluka_Name
Soil_color
```

Categorical features are transformed using:

```python
OneHotEncoder(handle_unknown='ignore')
```

The encoded categorical features are combined with the numerical features before training the Random Forest model.

---

# 🧠 Model Training Pipeline

```text
Raw Dataset
     │
     ▼
Data Cleaning
     │
     ▼
Feature Selection
     │
     ▼
Categorical Encoding
     │
     ▼
Feature Combination
     │
     ▼
Train/Test Split
     │
     ▼
Random Forest Classifier
     │
     ▼
Model Evaluation
     │
     ▼
Crop Prediction
```

The dataset is divided into training and testing subsets using:

```python
train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

The Random Forest model is configured with:

```python
RandomForestClassifier(
    n_estimators=100,
    random_state=42
)
```

---

# 🎥 YouTube Recommendation System

A new feature has been added to provide educational resources after prediction.

The system dynamically creates a YouTube search query using:

```text
Predicted Crop
+
Recommended Fertilizer
+
Farming/Cultivation
```

For example:

```text
Wheat farming cultivation fertilizer Urea
```

The query is URL encoded using Python's:

```python
quote_plus()
```

and converted into a YouTube search URL.

### Example

If the model predicts:

```text
Crop: Wheat
Fertilizer: Urea
```

The generated search query becomes:

```text
Wheat farming cultivation fertilizer Urea
```

The user can then click:

**▶️ Watch Wheat Farming & Fertilizer Videos**

This approach intentionally generates a search page rather than storing a single hardcoded video URL, so the user can see current search results.

---

# 📁 Project Structure

A recommended repository structure is:

```text
Crop-and-fertilizer-Recommend-model-for-Amravati-MH/
│
├── dataset/
│   └── agricultural_dataset.csv
│
├── notebooks/
│   └── crop_fertilizer_recommendation.ipynb
│
├── README.md
│
├── requirements.txt
│
└── LICENSE
```

If the dataset or notebook uses different filenames, update the structure accordingly.

---

# 🛠️ Technology Stack

| Category               | Technology       |
| ---------------------- | ---------------- |
| Programming Language   | Python           |
| Machine Learning       | Scikit-learn     |
| Algorithm              | Random Forest    |
| Data Processing        | Pandas           |
| Numerical Computing    | NumPy            |
| User Interface         | IPyWidgets       |
| Visualization/Notebook | Jupyter Notebook |
| Data Encoding          | OneHotEncoder    |
| Educational Resources  | YouTube Search   |
| Version Control        | Git & GitHub     |

---

# 📊 Dataset

The dataset used in this project is based on agricultural and regional data collected from government sources. The data was compiled and organized specifically for developing a crop and fertilizer recommendation system for the Amravati region of Maharashtra.

The dataset contains information related to geographical regions, soil characteristics, nutrient levels, weather conditions, crops, and fertilizers.

🏛️ Data Source

The agricultural data was collected from official government sources and publicly available government reports/data resources.

The collected information was then cleaned, structured, and consolidated into a machine-learning-ready dataset for this project.

Data Attribution: The original agricultural information belongs to the respective government departments/organizations that published the source data. This project uses the data for educational, research, and machine-learning development purposes.
The dataset contains agricultural information related to different regions/talukas and includes information such as:

```text
Taluka
Soil Color
Nitrogen
Phosphorus
Potassium
pH
Rainfall
Temperature
Crop
Fertilizer
```

The project focuses particularly on agricultural conditions relevant to **Amravati, Maharashtra**.

### Dataset Processing

The dataset is loaded using Pandas:

```python
dataset = pd.read_csv("your_dataset.csv")
```

The categorical columns are encoded using:

```python
OneHotEncoder(
    handle_unknown='ignore',
    sparse_output=False
)
```

---

# 💻 Installation

## 1. Clone the Repository

```bash
git clone https://github.com/VedantDgit/Crop-and-fertilizer-Recommend-model-for-Amravati-MH-.git
```

## 2. Navigate to the Project

```bash
cd Crop-and-fertilizer-Recommend-model-for-Amravati-MH-
```

## 3. Create a Virtual Environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### Linux/macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

## 4. Install Dependencies

```bash
pip install pandas numpy scikit-learn ipywidgets jupyter
```

Or, if `requirements.txt` is available:

```bash
pip install -r requirements.txt
```

---

# ▶️ Running the Project

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
crop_fertilizer_recommendation.ipynb
```

Run the cells sequentially.

Then:

1. Select the **Taluka**.
2. Select the **Soil Color**.
3. Select **Nitrogen**.
4. Select **Phosphorus**.
5. Select **Potassium**.
6. Select **pH**.
7. Select **Rainfall**.
8. Select **Temperature**.
9. Click **Recommend Crop and Fertilizer**.

The system will display:

```text
Recommended Crop
Recommended Fertilizer
Model Accuracy
YouTube Farming Resources
```

---

# 🖥️ User Interface

The notebook provides an interactive interface using `ipywidgets`.

Example:

```text
Select Taluka:       [ Choose Taluka       ▼ ]

Soil Color:          [ Select Soil Color    ▼ ]

Nitrogen:            [ Select Nitrogen      ▼ ]

Phosphorus:          [ Select Phosphorus    ▼ ]

Potassium:           [ Select Potassium     ▼ ]

pH:                  [ Select pH            ▼ ]

Rainfall:            [ Select Rainfall      ▼ ]

Temperature:         [ Select Temperature   ▼ ]

       [ 🌾 Recommend Crop and Fertilizer ]
```

The available soil colors and numerical values are dynamically filtered according to the selected Taluka and soil color.

---

# 🔗 Dynamic Filtering

The application implements dependent dropdowns.

For example:

```text
Taluka
  ↓
Soil Color
  ↓
NPK / pH / Rainfall / Temperature
```

When a user selects a Taluka, the system retrieves only the soil colors available for that Taluka.

After selecting the soil color, the system retrieves the corresponding agricultural parameter values.

This makes the interface more consistent with the available dataset.

---

# 📈 Model Evaluation

The dataset is divided into:

```text
80% → Training Data
20% → Testing Data
```

The model is evaluated using the test dataset.

Example:

```python
accuracy = model_crop.score(X_test, y_test)

print(f"Model Accuracy: {accuracy * 100:.2f}%")
```

> **Note:** The displayed accuracy depends on the exact dataset, preprocessing, train/test split, and model configuration. Do not claim a fixed accuracy in the README unless it has been measured from the current version of the code.

---

# 📋 Example Output

```text
🌾 CROP & FERTILIZER RECOMMENDATION
=============================================

📍 Taluka: Example Taluka
🌱 Soil Color: Black

🧪 Nitrogen: 80
🧪 Phosphorus: 40
🧪 Potassium: 40

⚗️ pH: 6.8
🌧️ Rainfall: 800
🌡️ Temperature: 25

=============================================

🌾 Recommended Crop: Wheat
🧪 Recommended Fertilizer: Urea

📊 Model Accuracy: XX.XX%

🎥 Learn More on YouTube

▶️ Watch Wheat Farming & Fertilizer Videos
```

---

# 🔍 Important Implementation Detail

The updated model uses **all agricultural input features**:

```text
N
P
K
pH
Rainfall
Temperature
Taluka
Soil Color
```

This is an important improvement over a model that uses only:

```text
Taluka + Soil Color
```

Using all available agricultural features allows the model to incorporate both soil and environmental conditions when making a prediction.

---

# ⚠️ Limitations

This project is intended as an **educational and decision-support system**, not as a replacement for professional agricultural advice.

Current limitations include:

* Dataset size may affect model generalization.
* Recommendations depend on the quality of the dataset.
* Weather conditions can change over time.
* Soil properties can vary within the same geographical region.
* Fertilizer recommendation is currently associated with the predicted crop rather than being independently optimized.
* YouTube results are dynamically generated search results and are not individually verified by the application.
* The model does not currently use real-time weather or soil sensor data.
* The system is primarily designed around the available Amravati-region dataset.

---

# 🔮 Future Enhancements

The project can be extended with:

### 🌦️ Real-Time Weather API

Integrate live:

* Temperature
* Rainfall
* Humidity
* Weather forecast

---

### 🌱 IoT Soil Sensors

Connect sensors to obtain:

* Real-time NPK
* Soil moisture
* Soil temperature
* pH

---

### 🗺️ Geographical Intelligence

Add:

* GPS-based location
* Taluka auto-detection
* Interactive maps
* District-level recommendations

---

### 🤖 Advanced ML Models

Compare Random Forest with:

* XGBoost
* LightGBM
* CatBoost
* Gradient Boosting
* Neural Networks

---

### 🧪 Independent Fertilizer Prediction

Instead of simply selecting a fertilizer associated with the predicted crop, build a separate fertilizer recommendation model using:

```text
Crop
N
P
K
pH
Soil Type
Weather
```

---

### 🌐 Web Application

Convert the notebook into a production web application using:

```text
Frontend
   ↓
React.js / Streamlit
   ↓
FastAPI / Flask
   ↓
ML Model
   ↓
Prediction
```

---

### 📱 Mobile Application

A future Android application could allow farmers to enter soil parameters directly from their smartphones.

---

### 🌍 Multi-District Support

The system can be expanded from Amravati to other districts of Maharashtra and eventually other regions of India.

---

# 💡 Applications

Potential applications include:

* 🌾 Crop selection assistance
* 🧑‍🌾 Farmer decision support
* 🌱 Agricultural education
* 🧪 Soil-based crop analysis
* 📊 Agricultural data analysis
* 🎓 Machine Learning academic projects
* 🏆 Hackathon projects
* 🔬 Agricultural research

---

# 🧪 Example Prediction Pipeline

Suppose a user enters:

```text
Taluka       → Example Taluka
Soil Color   → Black
Nitrogen     → 80
Phosphorus   → 40
Potassium    → 40
pH           → 6.8
Rainfall     → 800
Temperature  → 25
```

The model processes the input:

```text
Input Parameters
       ↓
Preprocessing
       ↓
One-Hot Encoding
       ↓
Random Forest
       ↓
Predicted Crop
       ↓
Associated Fertilizer
       ↓
YouTube Search Query
```

Final result:

```text
Crop → Predicted Crop
Fertilizer → Associated Fertilizer
YouTube → Farming Resource Search
```

---

# 📦 Dependencies

Recommended `requirements.txt`:

```text
pandas
numpy
scikit-learn
ipywidgets
jupyter
notebook
```

Install them with:

```bash
pip install -r requirements.txt
```

---

# 🔐 Data & Privacy

The project does not require personal user information for the prediction process.

The model works using agricultural input parameters provided by the user.

---

# 🤝 Contributing

Contributions are welcome.

To contribute:

```bash
git clone <repository-url>
```

Create a new branch:

```bash
git checkout -b feature/new-feature
```

Make your changes and commit:

```bash
git add .
git commit -m "Add new agricultural feature"
```

Push the branch:

```bash
git push origin feature/new-feature
```

Then create a Pull Request.

---

# 📜 License

This project can be distributed under the terms of the license included in the repository.

If no license has been added yet, consider adding an appropriate open-source license before publishing the project for reuse.

---

# 👨‍💻 Author

## Vedant Deshmukh

**B.Tech Computer Science Engineering — Artificial Intelligence & Machine Learning**

VIT Bhopal University

### GitHub

**VedantDgit**

---

# ⭐ Support

If you found this project useful:

⭐ Star the repository
🍴 Fork the repository
🐛 Report issues
💡 Suggest improvements

---

# 📌 Disclaimer

> This project is developed for educational, research, and decision-support purposes. Crop and fertilizer recommendations should be validated with local agricultural experts, soil testing, and current farming conditions before making real-world decisions.

---

## 🌾 Project Summary

**Crop & Fertilizer Recommendation System** combines:

```text
Agricultural Data
       +
Machine Learning
       +
Random Forest
       +
Soil Analysis
       +
Weather Parameters
       +
Taluka Information
       +
Fertilizer Recommendation
       +
YouTube Educational Resources
       =
Smart Agricultural Decision Support System
```

**Built with Python, Pandas, NumPy, Scikit-learn and IPyWidgets.**


