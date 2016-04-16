## Hărți pe web - elemente de bază

### resurse
* QGIS
* mapshaper.org
* Leaflet
* FileZilla

### exemplu - cafenele din Cluj
```html
<!doctype html>
<meta charset="utf-8">
<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet/v0.7.7/leaflet.css">
<style>
html, body, #map { height: 100%; margin: 0 }
</style>
<body>
<div id="map"></div>
<script src="http://cdn.leafletjs.com/leaflet/v0.7.7/leaflet.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.3/jquery.min.js"></script>
<script>
var map = L.map('map').fitBounds([[43, 20], [49, 30]]);

L.tileLayer("https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png", {attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, &copy; <a href="http://cartodb.com/attributions">CartoDB</a>'}).addTo(map);

var cluj = L.geoJson().addTo(map);
$.getJSON('cluj.geojson', function(data) {
  cluj.addData(data);
  map.fitBounds(cluj.getBounds());
});

</script>
```

### pregătit GeoJSON
* deschis vector layer în QGIS
* editat, simplificat
* layer > save as
  * Format: GeoJSON
  * CRS: WGS-84
  * encoding: utf-8

### WMS
```javascript
L.tileLayer.wms("http://www.geo-spatial.org/geoserver/ows?service=wms&version=1.1.1&request=GetCapabilities", {
  layers: 'geospatial:planuri_tragere_20k',
  format: 'image/png',
  transparent: true,
  attribution: "geo-spatial.org"
}).addTo(map);
```

### Upload pe server
* conectare
  * host: geo.grep.ro
  * username: radu
  * password: radu
  * port: 22
* remote site: `/home/radu/www`
* click dreapta, "create directory"
* drag and drop fișierele locale
* server la http://geo.grep.ro

### embed într-o pagină
```html
<iframe src="http://geo.grep.ro/mgax/cluj.html" style="border: 0; width: 500px; height: 300px"></iframe>
```
