<template>
  <div id="app">
    <div class="map-container">
      <MapComponent />
    </div>
    <div class="population-density-container">
      <PopulationDensityMap />
    </div>
  </div>
</template>

<script>
import MapComponent from './components/MapComponent.vue';
import PopulationDensityMap from './components/PopulationDensityMap.vue';

export default {
  components: {
    MapComponent,
    PopulationDensityMap,
  },
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.map-container,
.population-density-container {
  flex: 1;
  padding: 20px;
  background-color: rgb(255, 255, 255);
}
</style>
