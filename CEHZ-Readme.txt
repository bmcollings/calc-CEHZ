Ben Jones + Ben Collings
# Transect Analysis Pipeline

## Overview
This repository contains a Python script for automatically calculating CEHZS analyzing transect data in the context of wave points, bathymetry, and elevation. The script utilizes various geospatial libraries such as pandas, geopandas, rasterstats, rasterio, and shapely.

Wave data: https://coastalhub.science/
LiDAR: https://data.linz.govt.nz/layer/110757-northland-lidar-1m-dem-2018-2020/
https://data-niwa.opendata.arcgis.com/datasets/a2582b1eb3584237a3b50418f379ca84

## Installation
To run the script, make sure you have the required dependencies installed. You can install them using the following commands:

Libraries:
pip install pandas geopandas rasterstats rasterio tqdm


## Usage

### Step 1 - Find Nearest Wave Point for Each Transect
1. Import required modules.
2. Read transect points into a GeoDataFrame and clean up.
3. Set the engine to pyogrio.
4. Define a list of attributes to keep.
5. Read wave data, including DoC, into a GeoDataFrame.
6. Perform a nearest spatial join to find the nearest wave point for each transect.

### Step 2 - Create .shp for Transects from Intersection to Wave Point
1. Create a new GeoDataFrame where the geometry is a LineString from transect intersect to wave point.
2. Define a function to generate LineString geometry.
3. Create a new column containing LineString from transect to wave point.
4. Store intersect.
5. Set geometry to transect_wp LineString.
6. Tidy up GeoDataFrame and set geometry to transect.

### Step 3 - Find Depth Values
1. Define functions to find depth corresponding to closure depth and calculate length between points.
2. Create a GeoDataFrame to find the length of each transect from elevation to depth.
3. Redefine geometry from bathy_depth to eov_point and set as geometry.
4. Calculate the length of each transect.

### Step 4 - Calculate Elevation Based on EOV Point
1. Define a function to find EOV elevation from LIDAR.
2. Create a point from x, y coordinates.
3. Perform a point query using rasterstats, returning the elevation value.

### Additional Steps
1. Read in and join LIDAR tile IDs.
2. Perform spatial joins to get tile IDs and find bathy points within transect buffers.
3. Iterate over transects, find bathymetry depth and length, and save the results to a CSV file.

## Note
- Make sure to customize file paths and adjust parameters as needed within the script.

## License
This project is licensed under the [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/).