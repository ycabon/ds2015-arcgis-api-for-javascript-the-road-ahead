<!-- .slide: data-background="firstslide.jpg" -->
#ArcGIS API for Javascript: Road-ahead
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
 - currently in a Map: 1 Layer === 1 DOM Node
 - Can't work
 - Solution?


 - Separate the business logic from the drawing logic.
 - New model: Map/Layers + View(s)/LayerViews
 - Communication model: events and properties watching
 - -> decoupling, clearer about what's going on when a property changes 


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


## Properties watching
 - get/set/watch with a custom mixin Accessor
 - get: get the value
 - set: set the value
 - watch: be notified when property changes


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
 - Will all extends Accessor
 - Shorter names
 - So far TiledLayer/WebTiledLayer/OSM, DynamicLayer, FeatureLayer
 - One collection of operational layers, for all types of operational layers
 - -> GraphicsLayer can be placed where you decide image layers!



## GroupLayer
 - New layer: GroupLayer
 - group layers together
 - visibility mode: 'exclusive', 'independent', 'inherit'
 - listMode: 'hide-children', 'hidden'
 - part of the webscene spec, demo with webscene viewer



## Collection
 - More or less like an Array
 - add/remove/find/forEach/map...
 - emit events when it changes with what has been added/removed/moved
 - used for layers, used for basemap layers, used for graphics



## Basemap
 - basemap is not part of the Map.layers
 - fully fledge class 'esri/Basemap'
 - contains 3 Collections: baseLayers, referenceLayers, elevationLayers
 - can be set with string for esri's basemap or custom Basemap instance.



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
 - generic functions like animateTo(target, options)
 - Viewpoint: common way to share between 2D/3D (part of webscene spec)



## Other
 - legacy dojo loader removed - AMD only
 - classes are properly cased: esri/Map, esri/Graphic, esri/layers/Layer
 - Simplifying Popup



## in short 4.0 final
 - brings 3D
 - makes 2D better
 - has a nicer/simpler API



## Future:
 - (Jeremy?)



### Future: Webmap/Webscene APIs
 - read AND write webmap/webscene
 - ... (jeremy?)



### Roadmap
 - 



# Questions