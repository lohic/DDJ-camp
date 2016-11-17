# Data-driven journalism camp
Data-driven journalism camp in Berlin, november 2016. Example files.

## Tools : ##

Code editor if needed:

- [http://www.sublimetext.com](http://www.sublimetext.com)
- [https://atom.io](https://atom.io)

Charts, timeline and other dataviz library or tools:

- [https://www.infogr.am](https://www.infogr.am)
- [https://cloud.highcharts.com](https://cloud.highcharts.com)
- [https://developers.google.com/chart/](https://developers.google.com/chart/)
- [http://timeline.knightlab.com](http://timeline.knightlab.com)
- [http://www.aeontimeline.com](http://www.aeontimeline.com)
- [https://d3js.org](https://d3js.org)
- [http://leafletjs.com](http://leafletjs.com)
- [https://github.com/Leaflet/Leaflet.markercluster](https://github.com/Leaflet/Leaflet.markercluster)
- [https://github.com/makinacorpus/Leaflet.TextPath](https://github.com/makinacorpus/Leaflet.TextPath)
- [https://github.com/bbecquet/Leaflet.PolylineDecorator](https://github.com/bbecquet/Leaflet.PolylineDecorator)
- [https://github.com/teralytics/Leaflet.D3SvgOverlay](https://github.com/teralytics/Leaflet.D3SvgOverlay)
- [http://geojson.io/](http://geojson.io/)
- [https://www.mapbox.com](https://www.mapbox.com)

## Google charts ##

To export chart has an image, and be able to download it

- [https://jsfiddle.net/eueygc2e/8/](https://jsfiddle.net/eueygc2e/8/) (bubble charts)
- [https://jsfiddle.net/e1auxam2/1/](https://jsfiddle.net/e1auxam2/1/) (bar charts) 
- [https://jsfiddle.net/eueygc2e/10/](https://jsfiddle.net/eueygc2e/10/) (bubble charts)

## Timeline ##

- [http://timeline.knightlab.com](http://timeline.knightlab.com)
- [link to the spreadsheet template (to save in your google drive)](https://drive.google.com/previewtemplate?id=1pHBvXN7nmGkiG8uQSUB82eNlnL8xHu6kydzH_-eguHQ&mode=public)

##Leaflet

###1 - simple leaflet ###

A simple leaflet starter file, with open street map data. Leaflet is an opensource map library, that can be used with external data (Openstreetmap or mapbox) or even bitmap pictures. For this last example 

###2 - geojson demo ###

Data downloaded from [refugeehackathon](https://github.com/refugeehackathon/refugeetransit-android/blob/master/testdata/refugee-help-map.geojson)

To be able to work with the file without a web server (online or offline), some modifications were brought to the file :
`var refugee_data=` was added at the start, in order to store the geojson in a __variable__
And we replaced the string `"UNKNOWN"` by `"Feature"` in a code editor such as sublime, but this can be done in any tiny text editor with a search/replace functionnality.

Then we added 2 parts in the code :

- That part go before the script tag with the javascript code

```javascript
<!-- this is the link to the modified geojson -->
<script src="refugee_help_map.geojson" type="text/javascript"></script>
```

- That one goes after the map declaration in the javascript part

```javascript
// this is scanning the geojson file
L.geoJSON(refugee_data, {
	style: function(feature) {},
	onEachFeature: forEachPointFinded //this is the call to a function for each point
}).addTo(map);

// this is the declaration of the function forEachPointFinded
function forEachPointFinded(feature, layer) {
	// if a description is found
	if (feature.properties.description) {
		// we add a popup on the click event
		// the content of the popup is the Name and the description
		layer.bindPopup("<h1>"+feature.properties.Name+"</h1><div>"+feature.properties.description+"</div>");
	}
}
```

For more complicated ways to include geojson, you may read this article :
[External GeoJSON and Leaflet: The Other Way(s)](http://lyzidiamond.com/posts/external-geojson-and-leaflet-the-other-way)

### 3 - polyline styling ###

A polyline is geometrical linear path, composed of differents points. Here is the code to include a polyline :

```javascript
// this is how to add a line composed of differents points
var polyline  = L.polyline( [
		[52.354659, 13.028051], // 1st point
		[52.707861, 13.696250]	// 2nd point, ...
	],
	{
		color: 'red', 			// color
		weight:4,				// weight of the line
		opacity:0.5				// opacity of the line
	}
).addTo(map);					// we add it on the map
```
