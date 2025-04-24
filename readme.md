# Crop Yield Prediction Project

## Description
This project aims to predict crop yield (hg/ha_yield) based on various factors such as geographical area, year, average rainfall, pesticide usage, and average temperature. It includes a Jupyter Notebook for data analysis and model training, and a Flask web application to serve the trained model for predictions.

## Data
The primary dataset used is `yield_df.csv`. It contains crop yield data along with the following features:
* Area: The country or region
* Item: The type of crop
* Year: The year of the record
* average_rain_fall_mm_per_year: Average rainfall in mm per year
* pesticides_tonnes: Tonnes of pesticides used
* avg_temp: Average temperature
* hg/ha_yield: The crop yield in hectograms per hectare (target variable)

## Methodology (`CropYield-Prediction.ipynb`)
1.  **Data Loading & Preprocessing:** The `yield_df.csv` dataset is loaded using pandas. Preprocessing steps include dropping unnecessary columns, handling duplicates, and converting data types.
2.  **Exploratory Data Analysis (EDA):** The notebook includes basic analysis and visualization of the data.
3.  **Feature Engineering:** Categorical features (Area, Item) are converted to numerical using One-Hot Encoding. Numerical features are scaled using StandardScaler. A ColumnTransformer is used to apply these transformations.
4.  **Model Training & Selection:** The data is split into training and testing sets. Several regression models (Linear Regression, Lasso, Ridge, Decision Tree Regressor) are trained and evaluated based on Mean Absolute Error (MAE) and R2 score. The Decision Tree Regressor (`dtr`) showed the best performance and was selected as the final model.
5.  **Model Saving:** The trained Decision Tree model and the preprocessor object are saved using pickle (`dtr.pkl`, `preprocessor.pkl`) for later use in the web application.

## Web Application (`app.py`, `templates/index.html`)
* A simple web application is built using Flask.
* It loads the saved `dtr.pkl` model and the `preprocessor.pkl` object.
* It provides a user interface (`index.html`) where users can input the required features (Year, Rainfall, Pesticides, Temperature, Area, Item).
* Upon submission, the application preprocesses the input data using the loaded preprocessor and predicts the crop yield using the loaded Decision Tree model.
* The predicted yield is displayed back to the user.

## Installation & Setup
1.  **Clone the repository:**
    ```bash
    git clone <your-repo-url>
    cd Crop-Yield-Final-Project
    ```
2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate # On Windows use `venv\Scripts\activate`
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    *(Dependencies listed in `requirements.txt`: blinker, click, colorama, Flask, itsdangerous, Jinja2, joblib, MarkupSafe, numpy, pandas, python-dateutil, pytz, scikit-learn, scipy, six, threadpoolctl, tzdata, Werkzeug)* 

## Usage
1.  **Run the Flask application:**
    ```bash
    python app.py
    ```
2.  **Open your web browser** and navigate to the URL provided (usually `http://127.0.0.1:5000`).
3.  **Enter the required details** into the form on the web page.
4.  **Submit the form** to get the predicted crop yield.