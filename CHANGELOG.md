# Changelog

## Beta 7

#### Breaking Changes

* Task methods that accecpt callbacks (like `run` or `bounds`) now return and instance of `XMLHttpRequest` as opposed to the task or service.
* 

#### Changes

## Beta 6

#### Breaking Changes

* `L.esri.Tasks.Identify` has been renamed to `L.esri.Tasks.IdentifyFeatures`. This is to reduce confusion with `L.esri.Tasks.IdentifyImage` and to clearly delineate what these 2 classes do.

#### Changes
* Logo position can now be controlled by using the `logoPosition` option on `L.esri.BasemapLayer` https://github.com/Esri/esri-leaflet/issues/210
* Logo can now be hidden entirely and re-added to the map with the `L.esri.Controls.Logo` class. **If you use Esri map tiles you must display the Esri Logo!**
* Fix a regression from Beta 4 where features could not be loaded from ArcGIS Server if they were in non-mercator references. https://github.com/Esri/esri-leaflet/issues/283 https://github.com/Esri/esri-leaflet/pull/322
* The `addFeature`, `removeFeature`, `updateFeature` methods will no longer throw errors when callbacks are omitted. https://github.com/Esri/esri-leaflet/issues/285
* `deleteFeature` now properly removes the feature from the map so it will now appear after zooming or panning. https://github.com/Esri/esri-leaflet/issues/284
* New `createfeature`, `addfeature` and `removefeature` events on `L.esri.FeatureLayer`. https://github.com/Esri/esri-leaflet/issues/282
* `L.esri.Tasks.Query` now supports Map Services and Image Services with the new `query.layer(id)` and `query.pixelSize(point)` params respectively
* New `L.esri.Tasks.Find` task for searching feature text in Map Services https://github.com/Esri/esri-leaflet/pull/287. Thanks @rdjurasaj-usgs!
* Support for image services via `L.esri.Layers.ImageMapLayer`. Thanks @rdjurasaj-usgs and @tomwayson
* `L.esri.Tasks.IdentifyImage` for identifying images. Thanks @tomwayson.

#### Misc
* [New example](esri.github.io/esri-leaflet/examples/parse-feature-collection.html) for parsing [Feature Collections](http://resources.arcgis.com/en/help/arcgis-rest-api/#/featureCollection/02r30000003m000000/) from ArcGIS Online.
* [New example]() for labeling points with [Leaflet.label](https://github.com/Leaflet/Leaflet.label).
* Travis CI is now running tests https://github.com/Esri/esri-leaflet/pull/271
* Build are no longer saved in the `/dist` folder. https://github.com/Esri/esri-leaflet/pull/307
* [Development Roadmap](https://github.com/Esri/esri-leaflet/wiki/Roadmap) has been updated.

## Beta 5

#### Breaking Changes

* `Oceans` no longer contains map labels, labels have been added as another key `OceansLabels`.
* `L.esri.FeatureLayer` no longer inherits from `L.GeoJSON` and as a result no longer has `getBounds`, `bringToBack` or `bringToFront` or `addData` methods.
* L.esri.Util.geojsonBounds has been removed. If you need to get the bounding box of a GeoJSON object please use [Terraformer](http://terraformer.io) or [`L.GeoJSON`](http://leafletjs.com/reference.html#geojson).
* Many other utility methods have been removed. If you were using methods in the `L.esri.Util` namespace please check that they exist.
* Layers no longer fire a `metadata` event. They now have a `metadata` method that can be used to get layer metadata. If you need to convert extents into L.LatLngBounds you can use `L.esri.Util.extentToBounds`.
* `L.esri.DynamicMapLayer` no longer inherits from `L.ImageOverlay` as a result the `setUrl` method no longer exists.
* You can no longer pass a `cluster` object to `L.esri.ClusteredFeatureLayer`, instead pass any options you want to pass to `L.MarkerClusterGroup` directly to `L.esri.ClusteredFeatureLayer`.
* You can no long pass a string for the `layerDefs` option on `L.esri.DynamicMapLayer`. Layer definitions should now be passed as an object like `{'0':'STATE_NAME='Kansas' and POP2007>25000'}`
* You can no longer pass a string for the `layers` option on `L.esri.DynamicMapLayer` you can now only pass an array of layer ids that will be shown like `[0,1,2]`.
* The `createMarker` method on `L.esri.ClusteredFeatureLayer` has been renamed to `pointToLayer`.

#### Changes

* Added `OceansLabels` to `L.esri.BasemapLayer`.
* `Oceans` has switched to the new Ocean basemap with out labels.
* `L.esri.FeatureLayer` has been refactored into several classes. `L.esri.FeatureGrid` and `L.esri.FeatureManager` now handle loading and querying features from the service.
* `L.esri.ClusteredFeatureLayer` and `L.esri.HeatMapFeatureLayer` now inherit from `L.`L.esri.FeatureManager` so they share many new methods and options.
* `L.esri.FeatureLayer`, `L.esri.ClusteredFeatureLayer` and `L.esri.HeatMapFeatureLayer` now support time enabled service via `from`, `to`, `timeFields` and `timeFilterMode` options and `setTimeRange(from, to)` and `getTimeRange()` methods.
* `L.esri.FeatureLayer`, `L.esri.ClusteredFeatureLayer` and `L.esri.HeatMapFeatureLayer` now support `where` options and have new methods for `setWhere()` and `getWhere()` to perform filtering.
* `L.esri.FeatureLayer` now supports generalizing polygon and polyline features on the service side for performance using the new `simplifyFactor` option.
* Don't throw errors when `L.esri.BasemapLayer` is added to maps without an attribution control. If you do not add attribution you must handle adding attribution your self to the map.
* Remove rbush. Switch to tracking feature ids with the cell key system.
* Remove `L.esri.Util.geojsonBounds` as it was only being used to create bounds and envelopes for rbush.
* add `bindPopup` method to `L.esri.DynamicMapLayer`.
* add `getTimeRange` and `setTimeRange` methods `L.esri.DynamicMapLayer`.
* New `L.esri.Services` namespace to handle generic abstraction of interacting with ArcGIS Online and ArcGIS server services.
* new `L.esri.Services.Service` base class that can be used for interacting with any service. All `L.esri.Layers` classes now uses `L.esri.Services.Service` internally for their API requests. This class also abstracts authentication and proxying.
* new `L.esri.Services.FeatureLayer` class for interacting with the Feature Layer API.
* new `L.esri.Services.MapService` class for interacting with the Map Server API.
* new `L.esri.Tasks` namespace for tasks that map to individual API methods.
* new `L.esri.Tasks.Query` class for interacting with the Feature Layer query API.
* new `L.esri.Tasks.Identify` class for interacting with Map Servers that support identify.

## Beta 4 Patch 1

#### Changes

* Patches a bug with identifying features on DynamicMapLayer
* Various updates and fixes to examples

## Beta 4

#### New Demos
* Heat map layer - http://esri.github.io/esri-leaflet/heatmaplayer.html
* Geocoder - http://esri.github.io/esri-leaflet/findplaces.html

#### Changes

* Authentication for ClusteredFeatureLayer https://github.com/Esri/esri-leaflet/commit/d23ddd99ee86bb7255e4d89b6cf3f339a441c88b
* Removed Terraformer as a dependency to cut down on build size and complexity. The neccessary * * * Terraformer methods have been ported into L.esri.Util. This cuts a whomping 15kb from the build!
* Fix for DynamicMapLayer that is outside of min/max zoom levels https://github.com/Esri/esri-leaflet/commit/0d2c2c36ed6ccbad96e0ab24c24cc48f43079ade
* Fix for layerDefs in DynamicMapLayer https://github.com/Esri/esri-leaflet/commit/1375bbf2768ba0fb6806f51c09a3d6fa192521d9
* Add HeatmapFeatureLayer based on Leaflet.heat
* Add where and fields options to FeatureLayer and ClusteredFeatureLayer, and HeatmapFeatureLayer
* Add bounds property to the metadata event when possible #216

# Beta 3

* Improve DynamicMapLayer panning and zooming performance. #137
* FeatureLayer and ClusteredFeatureLayer can now load features from map services. Thanks to @odoe and @jgravois.
* FeatureLayer, DynamicMapLayer and ClusteredFeatureLayer all accept a token option for accessing services that require authentication and fire a `authenticationrequired` event when they encounter a need for a token. Thanks to @aaronpk for the Oauth demos. #139
* Add DarkGray and DarkGrayLabels to BasemapLayer. #190
* An attributionControl on maps is now required when using BasemapLayer. #159
