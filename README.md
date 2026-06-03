# Predicting PM2.5 Exposure in London Using Urban Spatial Features

This repository contains the project files for the Urban 5160 project report. The project examines whether basic urban spatial features can be used to predict PM2.5 exposure across London Output Areas (OAs). The analysis combines PM2.5 concentration data with London spatial boundary data and applies simple machine learning models, including Mean Baseline, Linear Regression, and Random Forest.

## Project Overview

PM2.5 is an important indicator of urban air pollution because it is closely related to public health and environmental exposure. In large cities such as London, pollution exposure is not evenly distributed across space. Some areas may experience higher PM2.5 levels because of their location, urban density, transport activity, or wider spatial context.

This project uses London Output Area-level PM2.5 data and GIS boundary data to explore the spatial distribution of PM2.5. It also builds prediction models using simple spatial features, such as area size, centroid coordinates, distance to central London, and borough information.

The main research question is:

**To what extent can basic urban spatial features predict PM2.5 exposure across London Output Areas?**

## Repository Contents

The repository contains the following files:

```text
report.ipynb
report.html
README.md
outputs/
```

The main files are:

* `report.ipynb`
  Jupyter Notebook containing Python code, analysis, visualisations, model results, and the written report.

* `report.html`
  HTML version exported from the Jupyter Notebook.

* `outputs/`
  Folder containing figures and output files generated during the analysis.

## Data Sources

This project uses two main public datasets from London Datastore.

### 1. PM2.5 data

The PM2.5 data were downloaded from London Datastore:

```text
https://data.london.gov.uk/dataset/pm25-map-and-exposure-data-29z1y
```

The dataset provides annual average PM2.5 concentration data for Greater London at the Output Area level. In this project, the PM2.5 value is used as the dependent variable for prediction.

### 2. London spatial boundary data

The spatial boundary data were downloaded from London Datastore:

```text
https://data.london.gov.uk/dataset/statistical-gis-boundary-files-for-london-20od9
```

The downloaded file is:

```text
statistical-gis-boundaries-london.zip
```

This zip file contains GIS boundary files for Greater London, including Output Area (OA), Lower Layer Super Output Area (LSOA), Middle Layer Super Output Area (MSOA), ward, and borough boundaries. This project uses the 2011 Output Area boundary shapefile because it matches the OA-level PM2.5 dataset.

## Data Download Instructions

To reproduce this project, download the data manually and place them in the project folder.

### Step 1: Download PM2.5 data

Go to the London Datastore PM2.5 page:

```text
https://data.london.gov.uk/dataset/pm25-map-and-exposure-data-29z1y
```

Download the PM2.5 CSV file and place it in the `data/` folder.

Example file path:

```text
data/OA2_PM25_2013.csv
```

### Step 2: Download London boundary data

Go to the London Datastore boundary data page:

```text
https://data.london.gov.uk/dataset/statistical-gis-boundary-files-for-london-20od9
```

Download the file:

```text
statistical-gis-boundaries-london.zip
```

Unzip the file and place the extracted folder inside the `data/` folder.

Example folder path:

```text
data/statistical-gis-boundaries-london/
```

The notebook will search this folder and read the 2011 Output Area shapefile using GeoPandas.

## Methods

The project follows a simple urban analytics workflow:

1. Load PM2.5 data and London Output Area boundary data.
2. Merge the two datasets using Output Area codes.
3. Clean the data by removing records with missing PM2.5 values.
4. Convert the spatial data to the British National Grid projected coordinate system.
5. Create spatial features, including:

   * OA area size
   * centroid x coordinate
   * centroid y coordinate
   * distance to central London
   * borough dummy variables
6. Explore PM2.5 distribution using descriptive statistics and visualisations.
7. Build and compare three prediction models:

   * Mean Baseline
   * Linear Regression
   * Random Forest
8. Evaluate model performance using:

   * Mean Absolute Error (MAE)
   * Root Mean Squared Error (RMSE)
   * R-squared (R²)
9. Interpret prediction results, feature importance, and spatial residual patterns.

## Python Packages

The project uses the following Python packages:

```text
pandas
geopandas
numpy
matplotlib
scikit-learn
shapely
```

These packages are used for data processing, spatial analysis, visualisation, and machine learning.

## Model Summary

Three models are compared in this project:

| Model             | Purpose                           |
| ----------------- | --------------------------------- |
| Mean Baseline     | Simple reference model            |
| Linear Regression | Interpretable benchmark model     |
| Random Forest     | Non-linear machine learning model |

The Random Forest model produced the strongest predictive performance in this project. This suggests that the relationship between PM2.5 exposure and basic spatial features is not fully linear.

## Main Findings

The analysis shows that basic urban spatial features can explain a large proportion of PM2.5 variation across London Output Areas. Linear Regression performs much better than the Mean Baseline, showing that spatial features contain useful predictive information. Random Forest performs best overall, indicating that non-linear modelling is more suitable for capturing small-area spatial variation in PM2.5 exposure.

The residual and error maps also show that some areas are harder to predict using only basic spatial features. This suggests that future work could improve the model by adding more detailed variables, such as road traffic, land use, green space, population density, and meteorological conditions.

## Limitations

This project has several limitations.

First, the PM2.5 data are from 2013, so the results mainly reflect the spatial pattern of air pollution in London at that time. They may not fully represent current pollution conditions.

Second, the model uses only basic spatial features derived from GIS boundary data. It does not include direct pollution source variables, such as traffic volume, road density, industrial land use, or weather conditions.

Third, the Random Forest model is used for prediction, not causal explanation. Feature importance shows which variables are useful for prediction, but it does not prove that these variables directly cause changes in PM2.5 concentration.

## How to Run the Notebook

To run the project:

1. Download the datasets using the links above.
2. Place the PM2.5 CSV file in the `data/` folder.
3. Place the extracted boundary folder in the `data/` folder.
4. Open the Jupyter Notebook:

```text
report.ipynb
```

5. Run all cells from top to bottom.
6. Export the notebook to HTML after running all cells.

The final HTML report should be submitted together with the notebook.

## References

Azmi, W. N. F. W., Pillai, T. R., Latif, M. T., Koshy, S., & Shaharudin, R. (2023). Application of land use regression model to assess outdoor air pollution exposure: A review. *Environmental Advances, 11*, 100353. https://doi.org/10.1016/j.envadv.2023.100353

Breiman, L. (2001). Random forests. *Machine Learning, 45*(1), 5–32. https://doi.org/10.1023/A:1010933404324

Greater London Authority. (2016). *PM2.5 map and exposure data*. London Datastore. https://data.london.gov.uk/dataset/pm25-map-and-exposure-data-29z1y

Greater London Authority. (n.d.). *Statistical GIS boundary files for London*. London Datastore. https://data.london.gov.uk/dataset/statistical-gis-boundary-files-for-london-20od9

Hoek, G., Beelen, R., de Hoogh, K., Vienneau, D., Gulliver, J., Fischer, P., & Briggs, D. (2008). A review of land-use regression models to assess spatial variation of outdoor air pollution. *Atmospheric Environment, 42*(33), 7561–7578. https://doi.org/10.1016/j.atmosenv.2008.05.057

World Health Organization. (2021). *WHO global air quality guidelines: particulate matter (PM2.5 and PM10), ozone, nitrogen dioxide, sulfur dioxide and carbon monoxide*. World Health Organization. https://www.who.int/publications/i/item/9789240034228
