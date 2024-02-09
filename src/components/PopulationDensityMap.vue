<template>
  <div class="population-density-map">
    <div id="population-density-maps">
      <l-map :zoom="zoom" :center="center" @load="onMapLoad">
        <l-tile-layer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"></l-tile-layer>
        <l-geo-json :geojson="usStatesGeoJSON" @add="onGeoJsonAdd"></l-geo-json>
      </l-map>
    </div>
    <div id="feature-info">
      <h2>Feature Information</h2>
      <div v-if="selectedFeature">
        <p>State: {{ selectedFeature.properties.name }}</p>
        <p>Population Density: {{ selectedFeature.properties.populationDensity }} people/sq mi</p>
      </div>
    </div>
  </div>
</template>

<script>
import { LMap, LTileLayer, LGeoJson } from 'vue3-leaflet';
import axios from 'axios';

export default {
  name: 'PopulationDensityMap',
  components: {
    LMap,
    LTileLayer,
    LGeoJson,
  },
  data() {
    return {
      zoom: 4,
      center: [37.8, -96],
      usStatesGeoJSON: null,
      selectedFeature: null,
    };
  },
  methods: {
    onGeoJsonAdd(event) {
      const geoJsonLayer = event.target;
      geoJsonLayer.eachLayer(layer => {
        const populationDensity = Math.random() * 100;
        const color = getColor(populationDensity);
        layer.setStyle({ fillColor: color, fillOpacity: 0.7 });
        layer.feature.properties.populationDensity = populationDensity;
        layer.on('click', this.onFeatureClick);
      });
    },
    onFeatureClick(event) {
      this.selectedFeature = event.target.feature;
    },
    onMapLoad() {
      axios.get('https://api.example.com/spatial-api')
        .then(response => {
          this.usStatesGeoJSON = response.data;
        })
        .catch(error => {
          console.error('Error fetching data:', error);
        });
    },
  },
};

function getColor(density) {
  return density > 80 ? '#800026' :
         density > 60 ? '#BD0026' :
         density > 40 ? '#E31A1C' :
         density > 20 ? '#FC4E2A' :
                        '#FD8D3C';
}
</script>

<style>
#app {
  display: flex;
  flex-direction: row;
}

#population-density-maps {
  flex: 1;
  height: 600px;
}

#feature-info {
  flex: 1;
  padding: 20px;
}


.population-density-map {
  background-color: #f0f0f0; 
  fill: #ff9900; 
  stroke: #333333; 
}

</style>
