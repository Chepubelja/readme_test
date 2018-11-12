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