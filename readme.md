# Assessment 3

## background
I made a data visualisation showing the average alcohol consumption per person per country in the year 2010.

## Process
When i started with the dataset I first wanted to use a bubble chart to represent the countries, but i quickly changed my mind an decided to use a world map to visualise the data. This seemed to be the best option because the data was about countries in the world.
The plan was to show a barchart with the stats of the country when a country was selected, but this wasn't feasible to make in the time frame for me so i decided to show the data in the tootltip.

## Changelog
To visualise the data I had there were som changes that needed to be made to the code.

First-off the code had a different way of making references, these where al predeclared in a config object at the start of the code

```
var config = {"data0":"Country (or dependent territory)","data1":"Population",
			 "label0":"label 0","label1":"label 1","color0":"#99ccff","color1":"#0050A1",
			 "width":960,"height":960}
```
I changed this data so that it would also reference to the extra data i would be needing from my csv an prettied it up a bit for readability.
As you can see i added 3 extra "datatypes" to represent the 3 subvalues of the dataset.
 ```
 var config = {
	 "data0": "country",
	 "data1": "total_litres_of_pure_alcohol",
	 "data2": "beer_servings",
	 "data3": "spirit_servings",
	 "data4": "wine_servings",
	 "label0": "label 0",
	 "label1": "label 1",
	 "color0": "#99ccff",
	 "color1": "#0050A1",
	 "width": 960,
	 "height": 960
 }
 ```


 For each of the datatypes i created i also added a MAP var to reference to the config
 ```
 //created variabeles referencing to te csv data linked in the config var
 var MAP_KEY = config.data0;
 var MAP_VALUE = config.data1;
 var MAP_BEERS = config.data2;
 var MAP_SPIRIT = config.data3;
 var MAP_WINE = config.data4;
 ```

after that i made a object for each value
```
var valueHash = {},
	beerHash = {},
	spiritHash = {},
	wineHash = {};
```
and updated the function which loops through the csv to ad data to each object which contains the country and a value.
```
data.forEach(function(d) {
	valueHash[d[MAP_KEY]] = +d[MAP_VALUE];
	beerHash[d[MAP_KEY]] = +d[MAP_BEERS];
	spiritHash[d[MAP_KEY]] = +d[MAP_SPIRIT];
	wineHash[d[MAP_KEY]] = +d[MAP_WINE];
});
```

then i added extra lines to the tooltip to show the extra data per country
```
.on("mousemove", function(d) {
	var html = "";
	html += "<div class=\"tooltip_kv\">";
	html += "<span class=\"tooltip_key\">";
	html += d.properties.name;
	html += "</span>";
	html += "<br>"
	html += "<span class=\"tooltip_value\">";
	html += (valueHash[d.properties.name] ? valueHash[d.properties.name] : "0");
	html += " Liters of alcohol";
	html += "</span>";
	html += "</div>";
```
+
```
html += "<br>"
//Add line with total beer consumption
html += "<span class=\"tooltip_value\">";
html += (beerHash[d.properties.name] ? beerHash[d.properties.name] : "0");
html += " beers consumed";
html += "</span>";
html += "<br>"
//Add line with total spirit consumption
html += "<span class=\"tooltip_value\">";
html += (spiritHash[d.properties.name] ? spiritHash[d.properties.name] : "0");
html += " spirits consumed";
html += "</span>";
html += "<br>"
//Add line with total wine consumption
html += "<span class=\"tooltip_value\">";
html += (wineHash[d.properties.name] ? wineHash[d.properties.name] : "0");
html += " wines consumed";
html += "</span>";
```
