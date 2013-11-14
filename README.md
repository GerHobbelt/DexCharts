# Introduction

DexCharts is a library which provides reusable charts for D3. DexCharts aims to provide:

* A variety of reusable charts and charting components to choose from.
* A framework for interconnecting these charts via listeners.

Future versions will include:

* More charts of course.
* More options and configurability on existing charts.
* Ability to cross over from D3JS to other frameworks such as ThreeJS/WebGL.
* Pluggable tool support.  IE: Charts will know enough about themselves to provide hints to tools so that they are easily integrated into visualization [tools such as Dex](http://dexvis.com/).  There is a method to my madness...

## Gallery

* [Bar Chart 1](http://dexvis.com/dexcharts/dist/2013.11.14/examples/BarChart1
.html)
* [Bar Chart 2](http://dexvis.com/dexcharts/dist/2013.11.14/examples/BarChart2
.html)
* [Bar Chart 3](http://dexvis.com/dexcharts/dist/2013.11.14/examples/BarChart3
.html)
* [Chord Chart 1](http://dexvis.com/dexcharts/dist/2013.11
.14/examples/Chord1
.html)
* [Chord Chart 2](http://dexvis.com/dexcharts/dist/2013.11
.14/examples/Chord2
.html)

## Usage

_**Step 1: Include D3**_

Make sure your HTML5 asset includes D3 like so:

```javascript
<script src="http://d3js.org/d3.v3.js"></script>
```

_**Step 2: Include DexCharts core**_

Now include the core DexCharts Javascript like so:

```javascript
<script src="../dex.js"></script>
```

_**Step 3: Include the specific components you will need:**_

Some components such as maps are quite large, so I decided that components should be required as needed instead of in one massive kitchen sink Javascript library.  Here, I am including a Bar Chart and a Horizontal Legend.

```javascript
<script src="../js/dex/component/d3/BarChart.js"></script>
<script src="../js/dex/component/d3/HorizontalLegend.js"></script>
```

_**Step 4: Include D3**_

Create one or more SVG containers for your charts::

Via html:

Or you can do it via html like this:

```html
<svg id="MyChart" width="1000" height="1000"></svg>
```

Or you can create the SVG in JavaScript code:

```javascript
var svg = d3.select("body").append("svg")
  .attr("id", "MyChart")
  .attr("width", 1000)
  .attr("height", 800)
  .append("g")
  .attr("transform", "translate(40,20)");
```

_**Step 5: Instantiate a chart**_

Next, we must configure and instantiate a chart.

```javascript
var mychart = new BarChart(
  {
    'parent' : '#MyChart',
    'csv'    :
    {
      'header' : [ "SALESMAN", "AGE", "SALES"],
      'data'   : [["BOB", 23, 1000], ["SUE", 32, 2000], ["PAT", 44, 3000]]
    }
  }
);
```

_**Step 6:**_

Render the chart.

```javascript
mychart.render();
```

### What else?

_**We can reconfigure and update our chart in one line.**_

This will change the simple bar chart to a grouped bar chart which will have columns for both AGE and SALES.

```javascript
mychart.attr("yi", [1, 2]).update();
```

_**We can create new charts from old charts.**_

Here we create a new chart called myotherchart from mychart.  It will inherit all parameters from the original.  Of course, this makes no sense, so we change the x/y offsets to display at a different location on the screen.

In two lines we are creating another permutation of a chart and rendering it!

```javascript
var myotherchart = new BarChart(mychart);
myotherchart.attr("yoffset", 400).render();
```

_**We can combine charts and tell them to listen to other another.**_

Here, we're telling our parallel coordinates chart (pcChart), to listen to our USStateMap named "map" when it generates a "selectState" event.  Data is passed through an object called chartEvent.

In this particular example, we're removing the old parallel lines chart, adding the selected state data to the data list, then updating the chart.  A live example of this visualization [US State Map wired to Parallel Coordinates](http://dexvis.com/vis/blog/2013/mar/reusable6/html/ParallelCoordinates3.html):

```javascript
map.addListener("selectState", pcChart, function(chartEvent)
  {
    if (stateMap[chartEvent.state] != null)
  	{
  	  d3.selectAll("#ParChart").remove();
  	  selectedStates[chartEvent.state] = true;

  	  var pcData = []
  	  
  	  for (var state in selectedStates)
  	  {
  	  	pcData.push(stateMap[state]);
  	  }
	  pcChart
	    .attr("normalize", pcData.length <= 1)
	    .attr("csv.data", pcData)
	    .attr("height", 200)
	    .update();
  	}
  });
```
# Available Charts

Currently, I am starting small for now.  There are a small set of useful components provided with this initial release.  Each component is highly configurable.  If one of these components does not do what you need, feel free to let me know.

Please download and explore the provided examples.

## Charts
### Bar Charts
![Bar Chart Example](http://dexvis.files.wordpress.com/2013/03/barchart1.png?w=688&h=715)
### Clustered Force Diagrams
![Clustered Force Example](http://dexvis.files.wordpress.com/2013/03/image29.png?w=611&h=567)
### Line Charts
![Line Chart Example](http://dexvis.files.wordpress.com/2013/03/reusabledemo2.png?w=640)
### Parallel Coordinates
![Parallel Coordinates Example](http://dexvis.files.wordpress.com/2013/03/image27.png?w=471&h=360)
### Pie Charts
![Pie Chart Example](http://dexvis.files.wordpress.com/2013/03/image21.png?w=386&h=411)
### Scatter Plots
![Scatter Plot Example](http://dexvis.files.wordpress.com/2013/03/scatterplot1.png?w=663&h=655)
## Maps
### US State Map
![US State Map Example](http://dexvis.files.wordpress.com/2013/03/image10.png?w=666&h=368)
### US County Map
![US County Map Example](http://dexvis.files.wordpress.com/2013/03/image32.png?w=621&h=343)
### World Country Map
![World Country Map Example](http://dexvis.files.wordpress.com/2013/03/image33.png?w=619&h=442)
## Legends
### Horizontal Legends
![Horizontal Legend](http://dexvis.files.wordpress.com/2013/03/horizontalordinallegend.png?w=636&h=170)
### Vertical Legends
![Vertical Legend](http://dexvis.files.wordpress.com/2013/03/image12.png?w=780&h=543)
