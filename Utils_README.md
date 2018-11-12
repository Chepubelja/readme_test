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