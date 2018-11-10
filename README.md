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
___calculate_acreage()___ - for calculating acreage for the mask with the given threshold.

---

```python 
def calculate_acreage(mask, threshold):
```
where:
- __mask__ is the path to the confidence mask.
- __threshold__ is the probability threshold (for e.g. `0.5`, `0.75`, `0.8`).


___calculate_counties_acreage()___ - for calculating acreage for all confidence masks of the county with the given threshold.
```python 
def calculate_counties_acreage(results_path, threshold, silent=False):
```
where:
- __results_path__ is the path to the folder with confidence masks of the needed county.
- __threshold__ is the probability threshold (for e.g. `0.5`, `0.75`, `0.8`).
- __silent__ is the boolean flag for printing the acreage with the given threshold.

### format_csv.py
> Sub-module for processing points given by China team.

### make_evolution_sentinel.py
> Sub-module for generating evolution of fields images.

### sentinel.py
> Sub-module for getting information about tiles which cover counties.

This file provides 2 functions:
- ___get_intersection()___ - for retrieving names of tiles from Sentinel that intersects with the state from input state `.shp` (shapefile).
- ___county_tiles_mapping()___ - for tiles-counties mapping and vice verse.

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
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### SQLhelper.py
> Sub-module for working with SQL-database.

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

