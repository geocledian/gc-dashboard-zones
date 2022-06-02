# gc-dashboard-zones
## Description
gc-dashboard-zones is an JavaScript/HTML app for visualizing the outputs of the ag|knowledge REST API from [geocledian](https://www.geocledian.com).
It is composed of various [Vue.js](https://www.vuejs.org) components from geocledian.

## Purpose
With this application you have an interactive map widget for visualizing outputs from the REST API of ag|knowledge from geocledian.com. gc-dashboard-zones may filter a set of parcels and show the zones product for the selected parcel both in a chart and a map.

## Integration
For the integration of the application you'll have to run the application with the provided init script `gc-dashboard-zones-init.js` which cares of loading dependent libraries like Vue, Leaflet, etc. **This is the recommended way!**

You have to add some dependencies in the head tag of the container website.
>Please ensure, that you load Vue.js (v.2.6.x) before loading the component first!
Also note that <a href="www.bulma.org">bulma.css</a> and <a href="www.fontawesome.org">Font awesome</a> wll be loaded through gc-dashboard-zones.css.


```html
<html>
  <head>

    <!--GC component begin -->

    <!-- loads also dependent css files via @import -->
    <link href="css/gc-dashboard-zones.css" rel="stylesheet">
    <!-- init script for components -->
    <script id="gc-dashboard-zones-init" type="text/javascript" src="js/gc-dashboard-zones-init.js" async></script>

    <!--GC component end -->
  </head>
```

Then you may create the widget(s) that build the whole application with custom HTML tags anywhere in the body section of the website. Make sure to use an unique identifier for each component. 

```html
<div id="gc-app">
    <gc-filter
        gc-widget-id="filter1"
        :gc-apikey="$root.gcApikey" 
        :gc-api-base-url="$root.gcApiBaseUrl"
        :gc-host="$root.gcHost"
        gc-layout="vertical"
        :gc-language="$root.language">
    </gc-filter>

  <gc-parcel-data 
        gc-widget-id="parceldata1"
        :gc-apikey="$root.gcApikey" 
        :gc-host="$root.gcHost"
        :gc-selected-parcel-id="$root.selectedParcelId"
        :gc-language="$root.language"
        gc-available-fields="parcelId,name,crop,entity,planting,harvest,area,promotion"
        gc-layout="horizontal">
  </gc-parcel-data>  

    <gc-zones-map
        gc-widget-id="map1"
        :gc-apikey="$root.gcApikey" 
        :gc-api-base-url="$root.gcApiBaseUrl"
        :gc-host="$root.gcHost"
        :gc-language="$root.language"
        gc-available-tools="legend,downloadImage"
        gc-selected-product="zones"
        :gc-current-parcel-id="$root.selectedParcelId" 
        gc-legend-position="topright"
        :gc-filter-string="$root.filterString"    
        :gc-limit="$root.limit"
        :gc-offset="$root.offset"
        :gc-data-source="$root.dataSource"
        :gc-startdate="$root.startdate"
        :gc-enddate="$root.enddate"
        :gc-pixelsize="$root.pixelsize"
    />
    <gc-zones-chart 
        gc-widget-id="zonesChart1"
        :gc-zones-data="$root.zonesData"
        gc-available-options=""
        :gc-white-label="true"
    />
</div>

```

## Support
The application is provided as is and we accept no liability for the source code. In case of bugs or questions please contact us at [us](mailto:info@geocledian.com). We are also happy to receive feedback. Unfortunately we can only offer very limited technical support, especially about integration in third party software.

## Used Libraries
- [Vue.js](https://www.vuejs.org)
- [Vue I18n](https://kazupon.github.io/vue-i18n/)
- [Leaflet](https://leafletjs.com/)
- [Leaflet Draw Plugin](http://leaflet.github.io/Leaflet.draw/docs/leaflet-draw-latest.html)
- [Leaflet GeoSearch Plugin](https://github.com/smeijer/leaflet-geosearch)
- [axios](https://github.com/axios/axios)
- [Bulma](https://bulma.io/documentation/)
- [Font awesome](https://fontawesome.com/)

## Legal: Terms of use from third party data providers
- You have to add the copyright information of the used data. At the time of writing the following text has to be visible for [Landsat](https://www.usgs.gov/information-policies-and-instructions/crediting-usgs) and [Sentinel](https://scihub.copernicus.eu/twiki/pub/SciHubWebPortal/TermsConditions/TC_Sentinel_Data_31072014.pdf) data:

```html
 contains Copernicus data 2021.
 U.S. Geological Service Landsat 8 used in compiling this information.
```

- this widget allows using data from the Google Maps API technically. Please ensure the complicance of the [terms of use](https://developers.google.com/maps/terms-20180207#7.-permitted-uses.) first before using them.

- this widget allows the technical integration of ArcGIS Online Services - e.g. as the [World Imagery Service](https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/). Please ensure the complicance of the [terms of use](https://www.esri.com/en-us/legal/terms/full-master-agreement) first before using them. 

**geocledian is not responsible for illegal use of third party services.**
