# System for Continous Airquality Prediction
Assignment *Lab 1* - ID2223 Scalable Machine Learning and Deep Learning, KTH Royal Institute of Technology
- By Isabel Grönquist (isgro@kth.se), and Kevin Kokalari (kokalari@kth.se)

## What it does

This assignment is about implemening a serverless and automatically running Machine Learning pipeline which predicts the air quality of Edinburgh using weather as well as current and historical PM 2,5 particle data measurements from different measurement stations in the city. More specifically, the modeling used particle measuremts from these measurement stations inside the city of Edinburgh:
- *Balmwell Terrace*
- *Salamander Street*
- *St John's Road*
- *St Leonards*
- *Tower Street*
- *Queensferry Road*


The pipeline in question: 
- Gets weather and air-quality data, 
- Uses these to create and store feature entries, 
- Trains a gradient boosting ML-model that builds an ensemble of decision trees (XGBoost), 
- Does batch predictions, and
- Presents the results in a simple webpage/dashboard.

Our pipeline also uses 1-day, 2-day, and 3-day lagging PM2.5 data included as features for the future air quality predictions being made. By adding these extra features, the performance of the prediction model increased significanlty resulting in a lower Mean Squared Error (MSE) when backtesting the predictions.


## Dashboard
[Result Dashboard](https://featurestorebook.github.io/mlfs-book/)


## Setting Up the Pipeline
See [Tutorial Instructions](https://docs.google.com/document/d/1YXfM1_rpo1-jM-lYyb1HpbV9EJPN6i1u6h2rhdPduNE/edit?usp=sharing)

```    
# Create a conda or virtual environment for your project
conda create -n book 
conda activate book

# Install 'uv' and 'invoke'
pip install invoke dotenv

# 'invoke install' installs python dependencies using uv and requirements.txt
invoke install
```

## Running the Pipeline with Multiple Air Quality Measurement Stations
To run this pipeline with data from multiple air quality measurement stations, the points below has to also be considered:
- All csv-files used to initialize the pipeline with air quality data must be stored under the data folder.
- In the .env file, the value of *AQICN_URL* has to be replaced with a single JSON-string with the keys being the measurement stations' api-urls, and the values being their identifiers. For example:
```python
'{"https://api.waqi.info/feed/@11656/": "tower street", "https://api.waqi.info/feed/@5986/": "salamander st"}'
 ```
- A trained XGBoost model will be trained, saved, and used to predict future air quality for every unique measurement station.
- Every unique air quality measurement station's ML-model will have its features saved in the same feature group and feature view, separated by the version number.


## Data Sources:
- Air Quality Data: [AQICN](https://aqicn.org/)
- Weather Data: [OPEN-METEO](https://open-meteo.com/)

