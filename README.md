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
- - -
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
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### natural.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### stitching.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

## Scripts
> Package contains four sub-modules:
- [calculate_acreage.py](#calculate_acreagepy) - for calculating acreage of fields for different probability thresholds using confidence masks.
- [format_csv.py](#format_csvpy) - for processing points given by China team.
- [make_evolution_sentinel.py](#make_evolution_sentinelpy) - for generating evolution of fields images.
- [sentinel.py](#sentinelpy) - for getting information about tiles which cover counties.
> and one `.ipynb` script:
- [Statistic.ipynb](#Statisticipynb) - for calculating statisics of counties.

### calculate_acreage.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### format_csv.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### make_evolution_sentinel.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### sentinel.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### Statistic.ipynb
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

## Utils
> Package contains four sub-modules:
- [azureUtil.py](#azureUtilpy) - for working with Azure Datalake.
- [sentinel_downloader.py](#sentinel_downloaderpy) - for blablabla.
- [SQLhelper.py](#SQLhelperpy) - for working with SQL-database.
- [utils.py](#utilspy) - small helper functions for different steps of pipeline.

### azureUtil.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### sentinel_downloader.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### SQLhelper.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

### utils.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.
