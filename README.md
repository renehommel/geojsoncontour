# geojsoncontour
[![Build Status](https://travis-ci.org/bartromgens/geojsoncontour.svg?branch=master)](https://travis-ci.org/bartromgens/geojsoncontour) [![PyPI version](https://badge.fury.io/py/geojsoncontour.svg)](https://badge.fury.io/py/geojsoncontour) [![Coverage Status](https://coveralls.io/repos/github/bartromgens/geojsoncontour/badge.svg?branch=master)](https://coveralls.io/github/bartromgens/geojsoncontour?branch=master)  
A Python 3 module to convert matplotlib contour plots to geojson. Supports both contour and contourf plots.

Designed to show geographical [contour plots](http://matplotlib.org/examples/pylab_examples/contour_demo.html),
created with [matplotlib/pyplot](https://github.com/matplotlib/matplotlib), as vector layer on interactive slippy maps like [OpenLayers](https://github.com/openlayers/ol3) and [Leaflet](https://github.com/Leaflet/Leaflet).

Demo project that uses geojsoncontour: [climatemaps.romgens.com](http://climatemaps.romgens.com)

## Forking notes

_This fork fixes issues with geojson style properties of the Leaflet/JS mapping library. The package converts matplotlib
contour plots to geojson files, which can be used in e.g. Folium (Python wrapper for Leaflet) or within Leaflet directly.
Here, particular emphasis is also given to a meaningful treatment of the time information of a transient/instationary/animated
contour plot in order to make animated interactive leaflet visualizations possible._


![geojson contour demo usage](https://raw.githubusercontent.com/bartromgens/geojsoncontour/master/data/example_climatemaps.png)

## Installation
Install with pip,
```
$ pip install geojsoncontour
```

## Usage

Use `contour_to_geojson` to create a geojson with contour lines from a `matplotlib.contour` plot (not filled).
Use `contourf_to_geojson` to create a geojson with filled contours from a `matplotlib.contourf` plot.

### Contour plot to geojson
```python
import numpy
import matplotlib.pyplot as plt
import geojsoncontour

# Create contour data lon_range, lat_range, Z
<your code here>

# Create a contour plot plot from grid (lat, lon) data
figure = plt.figure()
ax = figure.add_subplot(111)
contour = ax.contour(lon_range, lat_range, Z, cmap=plt.cm.jet)

# Convert matplotlib contour to geojson
geojson = geojsoncontour.contour_to_geojson(
    contour=contour,
    ndigits=3,
    unit='m'
)
```
For filled contour plots (`matplotlib.contourf`) use `contourf_to_geojson`.
See [example_contour.py](examples/example_contour.py) and [example_contourf.py](examples/example_contourf.py) for simple but complete examples.

### Show the geojson on a map
An easy way to show the generated geojson on a map is the online geojson renderer [geojson.io](http://geojson.io).

### Style properties
Stroke color and width are set as geojson properties following https://github.com/mapbox/simplestyle-spec.

### Create geojson tiles
Try [geojson-vt](https://github.com/mapbox/geojson-vt) or [tippecanoe](https://github.com/mapbox/tippecanoe) if performance is an issue and you need to tile your geojson contours.


## Tests

Run all tests,
```
python -m unittest discover
```
