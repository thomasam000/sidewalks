<template>
  <div class="hello">
    <div id="container">
      <div id="mapContainer" style="position:absolute; top:100px; bottom:0; left:0; right:0;">
      </div>
    </div>
   </div>
</template>

<script>
import 'leaflet/dist/leaflet.css'
import L from 'leaflet'
import jsonData from '../assets/Sidewalk(2).js'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
    // LMap, LTileLayer
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 13,
      center: [40.701452, -73.967923],
      mapDiv: null,
      polygons: []
    }
  },
  methods: {
    setupLeafletMap () {
      // const mapDiv = L.map('mapContainer').setView(this.center, 13)
      this.mapDiv = L.map('mapContainer', {
        center: this.center,
        zoom: this.zoom
      })
      L.tileLayer(this.url, {
        attribution: this.attribution
        // subdomains: ['a', 'b', 'c']
      }).addTo(this.mapDiv)
      // L.tileLayer(
      //   'http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      //   {
      //     attribution:
      //       'Map data (c) <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
      //     maxZoom: 18,
      //     id: 'mapbox/streets-v11',
      //     accessToken: 'XXX'
      //   }
      // ).addTo(mapDiv)
    }
  },
  mounted () {
    this.setupLeafletMap()
    console.log(jsonData.features[0])
    jsonData.features.forEach(shape => {
      var polygon = L.polygon(shape.geometry.coordinates, {color: 'blue'}).addTo(this.mapDiv);
      this.polygons.push(polygon)
    })
    this.mapDiv.fitBounds(this.polygons[0].getBounds());

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
