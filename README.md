🌾 CropSense AI – Crop Yield Prediction

A machine learning project that predicts crop yield from farm and weather details, and labels the result as Low, Medium or High. It includes a Gradio web app so anyone can try the model without writing code.

Built and run in Google Colab.

Features
Cleans and explores the crop yield dataset
Compares three regression models: Linear Regression, Random Forest and Bagging
Includes a Random Forest classifier for Low / Medium / High yield categories
Tunes the Bagging model with GridSearchCV and cross-validation
Saves trained models with joblib
Gradio web app with a clean interface and a colored result card
Dataset

File: crop_yield.csv (19,689 rows, 10 columns, years 1997–2020, no missing values)

Column	Description
Crop	Crop name (55 crops)
Crop_Year	Year of cultivation
Season	Kharif, Rabi, Summer, Autumn, Winter, Whole Year
State	Indian state (30 states)
Area	Cultivated area
Production	Total production
Annual_Rainfall	Rainfall in the year
Fertilizer	Fertilizer used
Pesticide	Pesticide used
Yield	Target – production per unit area

Production is not used as an input feature, because Yield is calculated from it.

Project Workflow
Upload and load the dataset
Check for missing values, duplicates and outliers
Clean the data (strip spaces, remove duplicates, fill missing values)
Explore with charts (top crops, rainfall vs yield, yield over years, correlation heatmap)
Build a preprocessing pipeline (OneHotEncoder for text columns, imputer and StandardScaler for numbers)
Train and compare models
Tune the best model and save it
Launch the Gradio app

Features used: Crop, Crop_Year, Season, State, Area, Annual_Rainfall, Fertilizer, Pesticide

Results

Test set = 20% of the data (random_state=42).

Model	R² Score	MAE
Linear Regression	0.81	63.9
Random Forest	0.98	9.6
Bagging (Decision Trees)	0.98	9.5

Random Forest classifier (Low / Medium / High) accuracy: about 88%.

Yield categories are made by splitting training yields into three equal groups (33rd and 67th percentiles), so the cutoffs are computed from the data and not typed in by hand.

Exact numbers can vary slightly between runs and library versions.

How to Run
Open the notebook ML_PROJECT.ipynb in Google Colab.
Run the cells from top to bottom.
When asked, upload crop_yield.csv.
Install Gradio and launch the app:
python
!pip install -q gradio

The last cell starts the app and prints a public link (share=True).

Using the App
Choose the Crop, Season and State
Enter the Crop Year, Area, Annual Rainfall, Fertilizer and Pesticide
Click Predict Yield
You get the predicted yield and a colored category badge:
🔴 Low
🟠 Medium
🟢 High

Tips for realistic input:

Fertilizer is usually about 100–190 times the Area, and Pesticide about 0.1–0.4 times the Area.
Change the crop and state, not only the numbers. The model depends mostly on the crop type.
Project Files
├── ML_PROJECT.ipynb            # Full notebook (cleaning, EDA, models, app)
├── crop_yield.csv              # Dataset
├── crop_yield_regression.pkl   # Saved Bagging model (created by the notebook)
└── crop_yield_classifier.pkl   # Saved classifier (created by the notebook)
Tech Stack

Python · pandas · NumPy · scikit-learn · matplotlib · seaborn · joblib · Gradio

Limitations
Coconut yield is measured in nuts (about 8,000 per unit area), while other crops range from about 0 to 150. This skews the regression and the category cutoffs.
The data only covers 1997–2020, so predictions for later years are extrapolations.
Predictions are estimates and not guaranteed crop outcomes.
Future Improvements
Train separate models for different crop groups
Add more weather features (temperature, soil type)
Deploy the app permanently (Hugging Face Spaces or Streamlit Cloud)
