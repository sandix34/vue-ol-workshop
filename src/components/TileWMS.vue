<template>
  <div id='map'></div>
</template>

<script>
// classes required to display the map
import Map from 'ol/Map'
import View from 'ol/View'
import OSM from 'ol/source/OSM'

import {Image as ImageLayer, Tile as TileLayer} from 'ol/layer'
import ImageWMS from 'ol/source/ImageWMS'

export default {
  methods: {
    initMap () {
      const layers = [
        new TileLayer({
          source: new OSM()
        }),
        new ImageLayer({
          // ImageWMS ---> https://openlayers.org/en/latest/apidoc/module-ol_source_ImageWMS-ImageWMS.html
          source: new ImageWMS({
            url: 'https://map.geomatick.com/geoserver/wms', // ---> this url does not work
            // url: 'https://ahocevar.com/geoserver/wms',        // ---> this url does work
            params: {'LAYERS': 'topp:states'},
            ratio: 1,
            serverType: 'geoserver',
            // crossOrigin: 'null'  // ---> the warnings disappear but the layer is not rendered
          })
        })
      ]

    const map = new Map({
        layers: layers,
        target: 'map',
        view: new View({
          center: [0, 0],
          zoom: 1
        })
      })
    }
  },
  mounted() {
    this.initMap()
  }
}
</script>


<style scoped>
@import '~ol/ol.css';
#map {
  height: 80vh;
  width: 80%;
  margin: auto;
}
</style>
