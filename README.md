GoogleMap AngularJS Directive
=============================

[![Build Status](https://travis-ci.org/allenhwkim/angularjs-google-maps.png?branch=master)](https://travis-ci.org/allenhwkim/angularjs-google-maps)

![Marker Cluster](http://i.imgur.com/tVEUg88.png)

[Demo](http://allenhwkim.github.io/angularjs-google-maps) &nbsp; &nbsp;
[Documentation](https://rawgithub.com/allenhwkim/angularjs-google-maps/master/build/docs/index.html)

There is already [one](https://github.com/nlaplante/angular-google-maps) for this. However, I found myself doing totally different approach for this purpose than the existing one, such as;

1. Everything in tag and attributes.   
   Basic users don't even have to know what Javascript is. Tag and attribute does it all.
2. Expose all original Google Maps V3 api to the user.  
   No hiding, no wraping, or whatsoever. 
   By doing so, programmers don't need to learn how to use this module.
   You only need to know Google Maps V3 API.

There is a blog that introduces this module. The title of it is '[Google Map As The Simplest Way](http://allenhwkim.tumblr.com/post/70986888283/google-map-as-the-simplest-way)'

To Get Started
--------------
For Bower users, 

  `$ bower install ngmap`

1. Include `ng-map.min.js` as well as google maps.  
    `<script src="http://maps.google.com/maps/api/js"></script>`  
    `<script src="http://rawgit.com/allenhwkim/angularjs-google-maps/master/build/scripts/ng-map.min.js"></script>`

2. name angular app as ngMap, or add it as a dependency

   `var myApp = angular.module('myApp', ['ngMap']);`

After map is initialized, you will have one event and map instances

Event:

  * `mapInitialized` with parameter with map

    In case your map directive scope is different from your controller scope,
    use this event to get the map instance.

    Example Usage:

    app.controller('parentParentController', function($scope) {
      $scope.$on('mapInitialized', function(event, map) {
        map.setCenter( .... )
        ..
      });
    });
    
Instances:

  * $scope.map
  * $scope.map.markers
  * $scope.map.shapes
  * etc

Directives
----------

#### **map** Directive

  As defined on [MapOptions](https://developers.google.com/maps/documentation/javascript/reference#MapOptions), you can add any attributes, and events starting witn `on-`. Please note that event value must be a function.

  Example: 

    <map zoom="11" 
      center="[40.74, -74.18]" 
      disable-default-u-i="true"
      disable-double-click-zoom="true"
      draggable="false"
      draggable-cursor="help"
      dragging-cursor="move"
      keyboard-shortcuts="false"
      max-zoom="12"
      min-zoom="8"
      tilt="45"
      map-type-id="TERRAIN">
    </map>
  i.e. < zoom="11" center="[40.74, -74.18]"

#### **marker** Directive

  As defined on [MarkerOptions](https://developers.google.com/maps/documentation/javascript/reference#MarkerOptions), you can add any attributes, and events starting witn `on-`.

    <map center="[40.74, -74.18]">
      <marker
          position="[40.76, -74.16]"
          title="Hello Marker"
          animation="Animation.BOUNCE"
          draggable="true"
          visible="true"
          icon="beachflag.png"></marker>
    </map>

#### **shape** Directive
It is used as a tag or an attribute.

     <map zoom="11" center="[40.74, -74.18]">
        <shape id="polyline" name="polyline" 
          geodesic="true" stroke-color="#FF0000" stroke-opacity="1.0" stroke-weight="2"
          path="[[40.74,-74.18],[40.64,-74.10],[40.54,-74.05],[40.44,-74]]" ></shape>
        <shape id="polygon" name="polygon" 
          stroke-color="#FF0000" stroke-opacity="1.0" stroke-weight="2"
          paths="[[40.74,-74.18],[40.64,-74.18],[40.84,-74.08],[40.74,-74.18]]" ></shape>
        <shape id="rectangle" name="rectangle" stroke-color='#FF0000' 
          stroke-opacity="0.8" stroke-weight="2"
          bounds="[[40.74,-74.18], [40.78,-74.14]]" editable="true" ></shape>
        <shape id="circle" name="circle" stroke-color='#FF0000'
          stroke-opacity="0.8"stroke-weight="2" 
          center="[40.70,-74.14]" radius="4000" editable="true" ></shape>
        <shape id="image" name="image" 
          url="https://www.lib.utexas.edu/maps/historical/newark_nj_1922.jpg"
          bounds="[[40.71,-74.22],[40.77,-74.12]]" opacity="0.7" clickable="true" ></shape>
     </map>

#### **info-window** Directive
Example:

    <map center="-25.363882,131.044922" zoom="4">
      <info-window id="bar" position="-25.363882,131.044922" visible="true">
        <div ng-non-bindable>
          <div id="siteNotice"></div>
        </div>
      </info-window>
    </map>

#### **custom-control** Directive
Example:

      <map center="41.850033, -87.6500523" zoom="6">
        <custom-control id="home" position="TOP_RIGHT" index="1" on-click="click()">
          <div style="background-color: black; color:#fff;cursor:pointer">Home1</div>
        </custom-control>
      </map>

#### **map-data** Directive
Example:

      <map zoom="4" center="-28, 137.883">
        <map-data 
          load-geo-json="https://storage.googleapis.com/maps-devrel/google.json"></map-data>
      </map>

### Layer Directives 

#### **bicycling-layer** Directive

      <map zoom="14" center="42.3726399, -71.1096528">
        <bicycling-layer></bicycling-layer>
      </map>

#### **weather-layer** Directive(deprecated) and **cloud-layer** Directive(deprecated)

      <map zoom="6" center="49.265984,-123.127491">
        <weather-layer temperature-units="FAHRENHEIT"></weather-layer>
        <cloud-layer></cloud-layer>
      </map>

#### **fusion-tables-layer** Directive

      <map zoom="11" center="41.850033, -87.6500523">
        <fusion-tables-layer query="{
          select: 'Geocodable address',
          from: '1mZ53Z70NsChnBMm-qEYmSDOvLXgrreLTkQUvvg'}">
        </fusion-tables-layer>
      </map>

#### **heatmap-layer** Directive

      <map zoom="13" center="37.774546, -122.433523" map-type-id="SATELLITE">
        <heatmap-layer id="foo" data="taxiData"></heatmap>
      </map>

#### **maps-engine-layer** Directive

      <map center="59.322506, 18.010025" zoom="14">
        <maps-engine-layer
          layer-id="06673056454046135537-08896501997766553811">
        </maps-engine-layer>
      </map>

#### **traffic-layer** Directive

      <map zoom="13" center="34.04924594193164, -118.24104309082031">
        <traffic-layer></traffic-layer>
      </map>

#### **transit-layer** Directive

      <map zoom="13" center="51.501904,-0.115871">
        <transit-layer></transit-layer>
      </map>

#### **dynamic-maps-engine-layer** Directive

      <map center="59.322506, 18.010025" zoom="14">
        <dynamic-maps-engine-layer
          suppress-info-windows="true"
          clickable="true"
          on-mouseover="onMouseover()"
          on-mouseout="onMouseout()"
          layer-id="06673056454046135537-08896501997766553811">
        </dynamic-maps-engine-layer>
      </map>

#### **kml-layer** Directive

      <map zoom="11" center="41.875696,-87.624207">
        <kml-layer url="http://gmaps-samples.googlecode.com/svn/trunk/ggeoxml/cta.kml"></kml-layer>
      </map>

### MapType Directives 

#### **map-type** Directive

      <map zoom="10" center="41.850033,-87.6500523"
        <map-type name="coordinate" object="CoordMapType">
        </map-type>
      </map>

#### **overlay-map-type** Directive

      <map zoom="10" center="41.850033,-87.6500523">
        <overlay-map-type object="CoordMapType" index="0">
        </overlay-map-type>
      </map>

Advanced Examples
-------------------
- [Marker Clusterer](https://rawgit.com/allenhwkim/angularjs-google-maps/master/testapp/marker-clusterer.html)
- [Starbucks World Wide](https://rawgit.com/allenhwkim/angularjs-google-maps/master/testapp/map_app.html)


license
=======

[MIT License](https://github.com/allenhwkim/angularjs-google-maps/blob/master/LICENSE)
