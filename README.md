# Map controller

Stateful map controller for Flutter Map. Manage markers, lines and polygons.

## Api

Api for the `StatefulMapController` class

### Map controls

#### Zoom

**`zoom`**: get the current zoom value

**`zoomIn()`**: increase the zoom level by 1

**`zoomOut()`**: decrease the zoom level by 1

**`zoomTo`**(`Double` *value*): zoom to the provided value

#### Center

**`center`**: get the current center `LatLng` value

**`centerOnPoint`**(`LatLng` *point*): center on the `LatLng` value

### Map assets

#### Markers

**`addMarker`**(`String` *name*, `Marker` *marker*): add a named marker on the map

**`addMarkers`**(`Map<String, Marker>` *markers*): add several named markers on the map

**`removeMarker`**(`String` *name*, `Marker` *marker*): remove a named marker from the map

**`removeMarkers`**(`Map<String, Marker>` *markers*): remove several named markers from the map

**`markers`**: get the markers that are on the map

**`namedMarkers`**: get the markers with their names that are on the map

#### Lines

**`addLine`**(`String` *name*,
          `List<LatLng>` *points*,
          `double` *width* = 1.0,
          `Color` *color* = Colors.green,
          `bool` *isDotted* = false): add a line on the map

**`lines`**: get the lines that are on the map

#### Polygons

**`addPolygon`**(`String` *name*,
          `List<LatLng>` *points*,
          `double` *width* = 1.0,
          `Color` *color* = const Color(0xFF00FF00),
          `double` *borderWidth* = 0.0,
          `Color` *borderColor* = const Color(0xFFFFFF00)): add a polygon on the map

**`polygons`**: get the polygons that are on the map

### On ready callback

Execute some code right after the map is ready:

   ```dart
   @override
   void initState() {
      statefulMapController.onReady.then((_) {
         setState((_) =>_ready = true);
      });
      super.initState();
   }
   ```

### Changefeed

A changefeed is available: it's a stream with all state changes from the map controller. Ex:

   ```dart
   import 'dart:async';

   StreamSubscription _changefeed;
   int _myzoom;

   statefulMapController.onReady.then((_) {
       _myzoom = liveMapController.zoom;
       _changefeed = liveMapController.changeFeed.listen((change) {
        if (change.name == "zoom") {
          setState(() {
              _myzoom = change.value;
          });
        }
      });
   }
