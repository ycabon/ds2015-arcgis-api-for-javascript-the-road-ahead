<!-- .slide: data-background="background_title.jpg" -->
#ArcGIS API for Javascript
#Road-ahead
Jeremy Bartley - Yann Cabon



## 3.x
 - Geometry Engine
 - Smart Mapping API
 - Image Server
 - ...



## 4.0
 - 2D/3D
 - multiple betas during 2015
 - API 4.0: new concepts & changes



## 2D/3D
 - Starting point of 4.0: 3D is coming!
 - currently in 3.x:
   - Map, many DOM nodes
   - Each Layer, 1 DOM Node
 - Can't work, WebGL renders in one Canvas
 - Solution?



## 2D/3D
 - Separate the business logic from the drawing logic.
![New model: Map/Layers + View(s)/LayerViews](architecture.png)
 - Communication model by __events__ and __properties watching__
   - clean decoupling
   - clearer about what's going on when something changes 



```javascript
var map = new Map({
  basemap: "topo"
});
map.add(new FeatureLayer(...));

/* create a 3D view for the Map */
var view = new View3D({
  map: map,
  container: "globeDiv"
});
```



## `esri/Accessor`
 - Mixin similar to `dojo/Stateful` with few differences
   - single object constructor
   - `get()` get a property value
   - `set()` set a property value
   - `watch()` be notified when property changes



## Properties watching
 - looks like dojo.Stateful with some changes
   - no support for setters returning a promise, for speed
   - watch callback signature is a bit different, because we care more about the new value.
 - Direct benefits:
   - remove inconsistancies, ctor, setter functions with parameters, no event for all properties etc...
   - one convention everywhere. You just need to know what property for which class
   - Single object constructor, no more 3+ constructors
   - Leaner SDK: we just have to doc the properties, the rest is conventional
 - Changes:
   - no more <property>-change events => watch()
   - watching for extent, not good since it changes all the time, new events for animation. 



## Layers

 - `map.layers`, a collection of the operational layers
   - mix of image AND graphics
 - Shorter names: `ArcGISTiledLayer`, `ArcGISDynamicLayer`
 - new ones:
   - `ArcGISElevationLayer`
   - `SceneLayer`
   - `GroupLayer`



## GroupLayer

 - New layer: GroupLayer
 - group layers together
 - visibility mode: `exclusive`, `independent`, `inherit`
 - listMode: 'hide-children', 'hidden'



## Collection

 - More or less like an Array
 - add/remove/find/forEach/map...
 - emit events when it changes with what has been added/removed/moved
 - used for layers, used for basemap layers, used for graphics



## Basemap

- full fledge class `esri/Basemap`
- basemap's layers are not part of the `map.layers`, but from `map.basemap`
- contains 3 Collections: baseLayers, referenceLayers, elevationLayers
- can be set with string for esri's basemap or custom Basemap instance.



## Basemap

 - `basemap` as a string, creation of the appropriated Basemap instance

  ```javascript
  var map = new Map({
    basemap: 'topo'
  });

  map.set('basemap', 'streets');
  ```

 - `basemap` as an instance of `Basemap`

  ```javascript
  var map = new Map({/*...*/});

  var toner = new Basemap({
    baseLayers: [
      new WebTiledLayer({
        urlTemplate
      })
    ]
  })

  map.set('basemap', 'streets');
  ```



## 2D
 - new "engine" in the work.
 - faster, more future proof
   - abstraction to draw tiles and dynamic images to ease custom layers/layerviews
   - abstraction to draw in DOM or Canvas, possibly webgl ;)
 - display graphics while zooming.
 - viewpadding
 - continous zoom
 - rotation



## 3D
 - webgl engine to display the earth.
 - z/m support in the API, tasks, layers...
 - support for simple symbols
 - new Symbols



## Animation
 - generic functions like `animateTo(target, options):Promise`
   - 
 - `esri/Viewpoint`: common way to share between 2D/3D



### Webmap & Webscene APIs
 - read
 - save
 - save as



## Other
 - legacy dojo loader removed - AMD only
 - classes are properly cased: esri/Map, esri/Graphic, esri/layers/Layer
 - Simplifying Popup



## Conclusion
 - One API
 - 3D, and better 2D
 - simplified API



<!-- .slide: data-background="background_title.jpg" -->
# Questions



<!-- .slide: data-background="background_title.jpg" -->
# Rate This Session
[www.esri.com/RateMyDevSummitSession](www.esri.com/RateMyDevSummitSession)