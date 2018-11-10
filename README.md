# Code explanation
This code (ХЗ ЯК ЦЕ НАЗВАТИ) contains 4 main packages ([Features](#Features), [Geoutils](#Geoutils), [Scripts](#Scripts), [Utils](#Utils)), which are described below.

## Features
> Package contains two sub-modules:
- [features.py](#featurespy) - for calculating features.
- [feature_vectors.py](#feature_vectorspy) - for transforming features into feature vectors.

### features.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

All indices are calculated in format:
```python
def index_name(bands, **args):
    # Code for calculating index
    return calculated_index, "Index name"
```
where:
- __bands__ is the dictionary of satellite image bands in format `{"B1": np.array, "B2": np.array, "B3": np.array}`.
- __**args__ are additional parameters used for index calculation (*for e.g.* `'gamma'`, `'alpha'`, `'beta'`). 

*Further these feature functions are used in [feature_vectors.py](#feature_vectorspy).*

### feature_vectors.py
> Sub-module for combining features into feature vectors for further feature extraction from points or satellite images for both training and prediction stages.

This file provides two functions for feature extraction:

---
___Version 0.1___ - for extracting point or image NDVI features.
```python 
def extract_one_channel_ndvi(period_name, bands, target):
```
where:
- __period_name__ is the string that specifies date where satellite images where taken (*for e.g.* `'20180603'`).
- __bands__ is the dictionary of satellite image bands in format `{"B1": np.array, "B2": np.array, "B3": np.array}`.
- __target__ is either `'image'` or `'point'`.

---

___Version 0.4___ - for extracting point or image vegetation features of specific zone.
```python 
def extract_new_features(period_name, bands, target, zone):
```
where:
- __period_name__ is the string that specifies date where satellite images where taken (*for e.g.* `'20180603'`).
- __bands__ is the dictionary of satellite image bands in format `{"B1": np.array, "B2": np.array, "B3": np.array}`.
- __target__ is either `'image'` or `'point'`.
- __zone__ is the string of zone name (*for e.g.* `'SentinelSouthZone1'`).
---
## Geoutils
> Package contains four sub-modules:
- [elevation.py](#elevationpy) - for processing binary masks of mountains.
- [masking.py](#maskingpy) - for processing prediction result masks.
- [natural.py](#naturalpy) - for processing nature water parks areas from `natural.shp`.
- [stitching.py](#stitchingpy) - for stitching original and predicted tiles into counties.

### elevation.py
> Sub-module for processing binary masks of mountains.

This file provides function that returns binary mask of area for which elevation is lower than threshold:

```python 
def get_elevation_mask(self, match_path, thresh):
```
where:
- __self__ is the instance of `class Elevator(Vars)`.
- __match_path__ is the path to satellite image file in `GeoTIFF` format (*for e.g.* `"sentinel_image.tif"`).
- __thresh__ is the threshold (*for e.g.* `1100`).


### masking.py
> Sub-module for processing prediction result masks.

### natural.py
> Sub-module for processing nature water parks areas from `'natural.shp'`.

This file provides function that returns binary mask of areas which are not water parks:

```python 
def get_nature_mask(self, match_path, erosion):
```
where:
- __self__ is the instance of `class Natural(Vars)`.
- __match_path__ is the path to satellite image file in `GeoTIFF` format (*for e.g.* `"sentinel_image.tif"`).
- __erosion__ is the level of erosion (*for e.g.* `2`).

### stitching.py
> Sub-module for stitching original and predicted tiles into counties.

## Scripts
> Package contains four sub-modules:
- [calculate_acreage.py](#calculate_acreagepy) - for calculating acreage of fields for different probability thresholds using confidence masks.
- [format_csv.py](#format_csvpy) - for processing points given by China team.
- [make_evolution_sentinel.py](#make_evolution_sentinelpy) - for generating evolution of fields images.
- [sentinel.py](#sentinelpy) - for getting information about tiles which cover counties.
> and one `.ipynb` script:
- [Statistic.ipynb](#Statisticipynb) - for calculating statisics of counties.

### calculate_acreage.py
> Sub-module for calculating acreage of fields for different probability thresholds using confidence masks.

This file provides 2 functions:
- ___calculate_acreage()___ - for calculating acreage for the mask with the given threshold.
- ___calculate_counties_acreage()___ - for calculating acreage for all confidence masks of the county with the given threshold.
---

```python 
def calculate_acreage(mask, threshold):
```
where:
- __mask__ is the path to the confidence mask.
- __threshold__ is the probability threshold *(for e.g.* `0.5`, `0.75`, `0.8`).

```python 
def calculate_counties_acreage(results_path, threshold, silent=False):
```
where:
- __results_path__ is the path to the folder with confidence masks of the needed county.
- __threshold__ is the probability threshold *(for e.g.* `0.5`, `0.75`, `0.8`).
- __silent__ is the boolean flag for printing the acreage with the given threshold.

### format_csv.py
> Sub-module for processing points given by China team.

This file provides 2 functions:
- ___dms2dec()___ - for converting coordinate values from Degrees Minutes Seconds (DMS) to Decimal Degrees (DD).
- ___combine_files()___ - for __ХЗ ДЛЯ ЧОГО__.

---

```python 
def dms2dec(dms_str):
```
where:
- __dms_str__ is the string with coordinate values in Degrees Minutes Seconds (DMS) format.

```python 
def combine_files(path, out):
```
where:
- __path__ is the input path to the folder with `.csv` files.
- __out__ is the path to `.csv`, where results would be written to.

### make_evolution_sentinel.py
> Sub-module for generating evolution of fields images.

This file provides 3 main functions:
- ___create_binary_mask()___ - for creating prediction binary mask with the threshold `0.5` and saving result in files with `GeoTIFF` format in both Black-and-White and RGB modes.
- ___create_confidence_mask()___ - for creating prediction confidence mask by combining 5 binary prediction masks at 5 different thresholds `[0.5, 0.6, 0.7, 0.8, 0.9]` and saving result in files with `GeoTIFF` format in both Black-and-White and RGB modes.
- ___evaluate()___ - for evaluating prediction results of the model (calculating predicted acreage) for the choosen county and saving both binary and confidence masks.

---

```python 
def create_binary_mask(self, name):
```
where:
- __self__ is the instance of `class ShapeMasker(Elevator, Natural)`.
- __name__ is the output name for the binary mask.

```python 
def create_confidence_mask(self, name):
```
where:
- __self__ is the instance of `class ShapeMasker(Elevator, Natural)`.
- __name__ is the output name for the confidence mask.

```python 
def evaluate(self, county, model_version):
```
where:
- __self__ is the instance of `class ShapeMasker(Elevator, Natural)`.
- __county__ is the name of the county *(for e.g.* `'Aksu'`).
- __model_version__ is the string representing current version of model *(for e.g.* `'0.1'`).


### sentinel.py
> Sub-module for getting information about tiles which cover counties.

This file provides 2 functions:
- ___get_intersection()___ - for retrieving names of tiles from Sentinel that intersects with the state from input state `.shp` (shapefile).
- ___county_tiles_mapping()___ - for tiles-counties mapping and vice versa.

---

```python 
def get_intersection(path_to_state, path_to_sentinel):
```
where:
- __path_to_state__ is the path to the state `.shp` (shapefile).
- __path_to_sentinel__ is the path to Sentinel all world tiles `.shp` (shapefile).

```python 
def county_tiles_mapping(shapes_path, counties_path, needed_counties):
```
where:
- __shapes_path__ is the path to Sentinel all world tiles `.shp` (shapefile).
- __counties_path__ is the path to the folder with all needed counties shapefiles.
- __needed_counties__ is the list of names of needed counties.


### Statistic.ipynb
> Script for calculating statisics of counties.

Using this script you can calculate number of points for each crop ___(for e.g. Cotton, Corn, Tomato)___ from the input `points.csv` and group them:
- by counties
- by path
- by row
- by path/row

To have this script working right, except `points.csv`, you should have:
- folder with all counties shapefiles (in the script it is `Counties Xinjiang`).
- shapefile with all paths/rows in the world (in the script it is `wrs2_descending.shp`).

## Utils
> Package contains four sub-modules:
- [azureUtil.py](#azureUtilpy) - for working with Azure Datalake.
- [sentinel_downloader.py](#sentinel_downloaderpy) - for blablabla.
- [SQLhelper.py](#SQLhelperpy) - for working with SQL-database.
- [utils.py](#utilspy) - small helper functions for different steps of pipeline.

### azureUtil.py
> Sub-module for working with Azure Datalake.

This file provides 3 functions:
- ___download_from_azure()___ - for downloading original tiles data from Azure Datalake.
- ___upload_to_azure()___ - for uploading data folder to Azure Datalake.
- ___download_preprocessed_tile()___ - if there is preprocessed tile data, downloads it from Azure Datalake.

---

```python 
def download_from_azure(self, tile, dates):
```
where:
- __self__ is the instance of `class AzureDownloaderUploader(Vars)`.
- __tile__ is the list containing tile name in format `["44","TVG"]`.
- __dates__ is the list of needed periods.

```python 
def upload_to_azure(self, in_folder, out_folder):
```
where:
- __self__ is the instance of `class AzureDownloaderUploader(Vars)`.
- __in_folder__ is the path to local folder you want to upload.
- __out_folder__ is the path to Azure folder, where you want to save __in_folder__.

```python 
def download_preprocessed_tile(self, local_folder, azure_folder):
```
where:
- __self__ is the instance of `class AzureDownloaderUploader(Vars)`.
- __local_folder__ is the path to local folder, where you want to save preprocessed tile data.
- __azure_folder__ is the path to Azure folder to download from.


### sentinel_downloader.py
> Sub-module for __Bla bla bla TODO.__

### SQLhelper.py
> Sub-module for working with SQL-database.

This file provides 3 functions:
- ___ds_connect()___ - for creating SQLAlchemy `Engine` and returning `Connection` object of this Engine .
- ___insert_estimation()___ - for inserting new county data in the DB.
- ___test_load_from_dest_db()___ - for testing if needed table would be retrieved from DB and SQL query would be executed correctly.

---

```python 
def ds_connect(self):
```
where:
- __self__ is the instance of `class DSDB(Vars)`.

```python 
def insert_estimation(self, county, period, area, clouds, avg_clouds, img_name):
```
where:
- __self__ is the instance of `class DSDB(Vars)`.
- __county__ is the name of the county *(for e.g.* `Korla`).
- __period__ is the ordinal number of period *(for e.g. `7`*).
- __area__ is the float number representing the estimated area for county *(for e.g. `13001.04`*).
- __clouds__ is the level of clouds *(for e.g.* `9`).
- __avg_clouds__ is the average level of clouds *(for e.g.* `3`).
- __img_name__ is the url for the image.

```python 
def test_load_from_dest_db(self):
```
where:
- __self__ is the instance of `class DSDB(Vars)`

### utils.py
> Sub-module with small helper functions for different steps of pipeline.

This file provides 3 helper functions:
- ___latlon_to_pixel()___ - for transforming latitude and longitude to the corresponding pixels on the satellite image.
- ___norm_band()___ - for normalizing input numpy array to interval [0-1].
- ___mask_padding()___ - for dilating areas in the mask filled with 1.

---

```python 
def latlon_to_pixel(transform, latlon, zone):
```
where:
- __transform__ is gdal GeoTransform of the satelite image.
- __latlon__ is list with latitude and longitude.
- __zone__ is Zone Number, which  is represented with global map numbers of an UTM Zone Numbers Map.

```python 
def norm_band(band):
```
where:
- __band__ is one band *(Numpy array)* of the satellite image.

```python 
def mask_padding(mask, padding):
```
where:
- __mask__ is the input binary mask.
- __padding__ is the number of times dilation is applied.

