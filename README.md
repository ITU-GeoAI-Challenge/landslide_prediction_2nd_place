# Second Place Solution to GEO-AI Challenge for Landslide Susceptibility Mapping by ITU

## Introduction
This repository contains the second-place solution to the GEO-AI Challenge for Landslide Susceptibility Mapping by ITU. Below, you'll find information about the data, features, and the solution's workflow.

## Data
Please begin by fetching the data from this [Google Drive link](https://drive.google.com/file/d/1bL9tU7F0CpMtmoUQ6JWbLSQCwa-CLIUY/view).

### Geospatial Vector Data
- Geological Faults: `geological_faults.gpkg`
- Land Use: `land_use_land_cover.gpkg`
- River Network: `river_network.gpkg`
- Road Network: `road_network.gpkg`
- Training Data: `Train.gpkg`
- Testing Data: `Test.gpkg`

### Tabular Data
- Training Data: `Train.csv`
- Testing Data: `Test.csv`

### Raster Data
- Digital Terrain Model (DTM): `dtm.tif`
- Average Precipitation 2020: `average_precipitation_2020.tif`
- 90th Percentile Precipitation 2020: `90_perc_precipitation_2020.tif`

## Output Data and Storage
### Intermediate Data
Various feature extraction and transformation steps produce intermediate data that's stored within variables and DataFrames (e.g., `dtm_data`, `landslides`, `no_landslides`, etc.).

### Final Data
The final output is a submission file containing the IDs of the test samples and their corresponding predicted targets. It's stored in a CSV file named `submission.csv`.

## Features Used
### A. Original Features
1. Geological Features:
   - The proximity of each sample to geological faults, river networks, and road networks is computed.
2. Geospatial Features:
   - Data from geopackage files include information about geological structures and land use.
3. Raster Data Features:
   - Values extracted from raster datasets like DTM, average precipitation 2020, and 90th percentile precipitation 2020.

### B. Engineered Features
1. Elevation:
   - Elevation data is extracted from the DTM raster file for both landslides and non-landslide locations.
2. Distance to Geological Features:
   - The distances to the nearest fault, river, and road are calculated for each sample.
3. Slope and Aspect:
   - Slope and aspect values are calculated from the DTM and added as features. Aspect values of -9999 are replaced with the median aspect value to handle erroneous or missing data.
4. X and Y Coordinates:
   - The x and y coordinates of each sample are extracted and used as features.
5. Handling Missing Data:
   - Missing values in features like average and 90th percentile precipitation are imputed using the mode value of each feature.

### C. Data Preprocessing and Model Training
1. Data Splitting and Standardization:
   - The dataset is split into training and testing sets, and features are standardized using StandardScaler.
2. Model Training:
   - A Random Forest Classifier is trained on the training data. The performance is evaluated using accuracy and a classification report, showcasing precision, recall, and F1-score for each class.

### D. Predictions and Submission
1. Predictions on Test Data:
   - The trained model is used to predict the test data. The test features are standardized using the scaler fitted on the training data before making predictions.
2. Submission File:
   - Predictions are saved along with the ID of each test sample in a CSV file named `submission.csv`.

## Additional Notes
- The data paths are hardcoded and need to be modified according to the actual data location on your system.
