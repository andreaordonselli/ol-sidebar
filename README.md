# ol-sidebar

A responsive sidebar for [OpenLayers](https://openlayers.org/) 10.6

![Video](doc/ol-sidebar.gif)

## Preview
Complete example code at [`examples/index.html`](examples/index.html) ([Preview](http://andreaordonselli.github.io/ol-sidebar/examples/index.html))

## Sidebar collapsed

![Sidebar collapsed](doc/ol-1.png) 

## Sidebar extended

![Sidebar extended](doc/ol-2.png)

## Usage

In your HTML ensure that you have loaded the [OpenLayers](https://openlayers.org/) and `ol-sidebar` CSS.
In the example code below we also use [FontAwesome](https://fontawesome.com/) so that nice symbols can be
used for the sidebar's buttons.

```HTML
    <link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/ol@10.6.1/ol.min.css" type="text/css">
    <link rel="stylesheet" href="../css/ol-sidebar.css" />
```

Then create the `div` element within the HTML `body` for the map similarly to how one would for plain OpenLayers maps.

```HTML
<div id="map"></div>
```

Now define the sidebar (by default in a collapsed state) via the `sidebar` and `collapsed` classes:

```HTML
<div id="sidebar" class="sidebar collapsed">
</div>
```

Each sidebar element consists of a navigation tab connected to a tab pane
containing the content of the sidebar element.

The navigation tabs are a simple unordered list of anchors linking to the
respective tab pane:

```HTML
  <!-- navigation tabs -->
  <div class="sidebar-tabs">
    <ul role="tablist">
      <li><a href="#home" role="tab"><i class="fa fa-bars"></i></a></li>
    </ul>
  </div>
```

The content of a given tab is contained in a sidebar tab pane (note the `id`
attribute pointing back to the relevant navigation tab).  A pane includes a
header (via the `sidebar-header` class), which contains the `span` element
needed to close the pane, and then simple HTML text, for instance `p`
elements:

```HTML
  <!-- tab panes -->
  <div class="sidebar-content">
    <div class="sidebar-pane" id="home">
      <h1 class="sidebar-header">
        Pane header text
        <span class="sidebar-close"><i class="fa fa-caret-left"></i></span>
      </h1>

      <p>Pane text</p>
    </div>
  </div>
```

Now that the HTML has been set up, we can add the sidebar to the OpenLayers
map within JavaScript by adding a `script` element at the end of the `body`.

Don't forget to load the OpenLayers and ol-sidebar JavaScript:

```HTML
<script src="https://cdn.jsdelivr.net/npm/ol@10.6.0/dist/ol.min.js"></script>
<script src="../js/ol-sidebar.js"></script>
```

Then set up the OpenLayers map, in this case using an
[OpenStreetMap](https://www.openstreetmap.org/) source:

```HTML
<script>
    var map = new ol.Map({
        target: 'map',
        layers: [
            new ol.layer.Tile({
                source: new ol.source.OSM()
            })
        ],
        view: new ol.View({
            center: ol.proj.transform([7, 51.2], 'EPSG:4326', 'EPSG:3857'),
            zoom: 4
        })
    });
</script>
```

To add the sidebar, simply create a new `Sidebar` object which links to the
sidebar `div` created above, and then add it as a new control to the map:

```javascript
    var sidebar = new Sidebar({
      element: 'sidebar',
      position: 'left'
    });
    map.addControl(sidebar);
```

Complete example code at [`examples/index.html`](examples/index.html) ([Preview](http://andreaordonselli.github.io/ol-sidebar/examples/index.html))

## License

[MIT license](LICENSE).
