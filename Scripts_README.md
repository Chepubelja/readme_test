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