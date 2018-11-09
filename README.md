# Code explanation
This code (ХЗ ЯК ЦЕ НАЗВАТИ) contains 4 main packages ([Features](#Features), [Geoutils](#Geoutils), [Scripts](#Scripts), [Utils](#Utils)), which are described below.

## Features
> Package contains two sub-modules:
- [features.py](#featurespy) - for calculating features.
- [feature_vectors.py](#featurespy) - for transforming features into feature vectors.

### features.py
> Sub-module for generating various vegetation, soil and water indices by appling linear and non-linear manipulations on satellite bands.

All indices are calculated in format:
```python
def index_name(bands, **args):
    # Code for calculating index
    return calculated_index, "Index name"
```
where __bands__ is the dictionary of satellite image bands and __**args__ are additional parameters used for index calculation. 

*Further these feature functions are used in [feature_vectors.py](#featurespy).*

### feature_vectors.py
> Sub-module for combining features into feature vectors for further feature extraction from points or satellite images for both training and prediction stages.

This file provides two functions for feature extraction:
* __Version 0.1__ - for extracting point or image NDVI features.
```python 
def extract_one_channel_ndvi(period_name, bands, target):
```
where:
    - __period_name__ is the string that specifies date where satellite images where taken
    - __bands__ is the dictionary of satellite image bands in format `{"B1": np.array, "B2": np.array, "B3": np.array}`
    - __target__ is either `'image'` or `'point'`


- __Version 0.4__ - for extracting point or image vegetation features of specific zone.
```python 
def extract_new_features(period_name, bands, target, zone):
```
where:
    - __period_name__ is the string that specifies date where satellite images where taken
    - __bands__ is the dictionary of satellite image bands in format `{"B1": np.array, "B2": np.array, "B3": np.array}`
    - __target__ is either `'image'` or `'point'`
    - __zone__ is the string of zone name (***for e.g.*** `'SentinelSouthZone1'`).
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
where __match_path__ is the path to file 


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



# Satelite image segmenation using Mask R-CNN

The goal of this project is to 
## Getting Started









Dillinger is a cloud-enabled, mobile-ready, offline-storage, AngularJS powered HTML5 Markdown editor.

  - Type some Markdown on the left
  - See HTML in the right
  - Magic

# New Features!

  - Import a HTML file and watch it magically convert to Markdown
  - Drag and drop images (requires your Dropbox account be linked)


You can also:
  - Import and save files from GitHub, Dropbox, Google Drive and One Drive
  - Drag and drop markdown and HTML files into Dillinger
  - Export documents as Markdown, HTML and PDF

Markdown is a lightweight markup language based on the formatting conventions that people naturally use in email.  As [John Gruber] writes on the [Markdown site][df1]

> The overriding design goal for Markdown's
> formatting syntax is to make it as readable
> as possible. The idea is that a
> Markdown-formatted document should be
> publishable as-is, as plain text, without
> looking like it's been marked up with tags
> or formatting instructions.

This text you see here is *actually* written in Markdown! To get a feel for Markdown's syntax, type some text into the left window and watch the results in the right.

### Tech

Dillinger uses a number of open source projects to work properly:

* [AngularJS] - HTML enhanced for web apps!
* [Ace Editor] - awesome web-based text editor
* [markdown-it] - Markdown parser done right. Fast and easy to extend.
* [Twitter Bootstrap] - great UI boilerplate for modern web apps
* [node.js] - evented I/O for the backend
* [Express] - fast node.js network app framework [@tjholowaychuk]
* [Gulp] - the streaming build system
* [Breakdance](http://breakdance.io) - HTML to Markdown converter
* [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

### Installation

Dillinger requires [Node.js](https://nodejs.org/) v4+ to run.

Install the dependencies and devDependencies and start the server.

```sh
$ cd dillinger
$ npm install -d
$ node app
```

For production environments...

```sh
$ npm install --production
$ NODE_ENV=production node app
```

### Plugins

Dillinger is currently extended with the following plugins. Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| Github | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |


### Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantanously see your updates!

Open your favorite Terminal and run these commands.

First Tab:
```sh
$ node app
```

Second Tab:
```sh
$ gulp watch
```

(optional) Third:
```sh
$ karma test
```
#### Building for source
For production release:
```sh
$ gulp build --prod
```
Generating pre-built zip archives for distribution:
```sh
$ gulp build dist --prod
```
### Docker
Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the Dockerfile if necessary. When ready, simply use the Dockerfile to build the image.

```sh
cd dillinger
docker build -t joemccann/dillinger:${package.json.version}
```
This will create the dillinger image and pull in the necessary dependencies. Be sure to swap out `${package.json.version}` with the actual version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on your host. In this example, we simply map port 8000 of the host to port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart="always" <youruser>/dillinger:${package.json.version}
```

Verify the deployment by navigating to your server address in your preferred browser.

```sh
127.0.0.1:8000
```

#### Kubernetes + Google Cloud

See [KUBERNETES.md](https://github.com/joemccann/dillinger/blob/master/KUBERNETES.md)


### Todos

 - Write MORE Tests
 - Add Night Mode

License
----

MIT


**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
