<template>
  <div id="map-container">
    <l-map :zoom="zoom" :center="center">
      <l-tile-layer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"></l-tile-layer>

     
      <l-marker
        v-for="(location, index) in locations"
        :key="index"
        :lat-lng="location.coordinates"
        @mouseover="showDetails(location)"
        @mouseout="hideDetails"
      >
        <l-popup>{{ location.name }}<br/>{{ location.description }}</l-popup>
      </l-marker>

      <!-- Display details -->
      <div v-if="displayDetails" class="location-details">
        <p>{{ selectedLocation.name }}</p>
        <p>{{ selectedLocation.description }}</p>
      </div>
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer, LMarker, LPopup } from 'vue3-leaflet';

export default {
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
  },
  data() {
    return {
      zoom: 5,
      center: [20.5937, 78.9629],
      locations: [
      { name: 'Mumbai', coordinates: [19.0760, 72.8777], description: 'Financial capital of India' },
      { name: 'Delhi', coordinates: [28.7041, 77.1025], description: 'Capital city of India' },
      { name: 'Bangalore', coordinates: [12.9716, 77.5946], description: 'Silicon Valley of India' },
      { name: 'Hyderabad', coordinates: [17.3850, 78.4867], description: 'City of Pearls' },
      { name: 'Ahmedabad', coordinates: [23.0225, 72.5714], description: 'Business hub in Gujarat' },
      { name: 'Chennai', coordinates: [13.0827, 80.2707], description: 'Gateway to South India' },
      { name: 'Kolkata', coordinates: [22.5726, 88.3639], description: 'Cultural capital of India' },
      { name: 'Surat', coordinates: [21.1702, 72.8311], description: 'Commercial center in Gujarat' },
      { name: 'Pune', coordinates: [18.5204, 73.8567], description: 'Oxford of the East' },
      { name: 'Jaipur', coordinates: [26.9124, 75.7873], description: 'Pink City of India' },
      { name: 'Adoni', coordinates: [15.6310, 77.2728], description: 'City in Andhra Pradesh' },
      { name: 'Amaravati', coordinates: [16.5748, 80.3578], description: 'New capital of Andhra Pradesh' },
      { name: 'Anantapur', coordinates: [14.6819, 77.6006], description: 'District in Andhra Pradesh' },
      { name: 'Chandragiri', coordinates: [13.4127, 79.1897], description: 'Town in Andhra Pradesh' },
      { name: 'Chittoor', coordinates: [13.2174, 79.1002], description: 'City in Andhra Pradesh' },
      { name: 'Dowlaiswaram', coordinates: [16.9990, 81.7787], description: 'Village in Andhra Pradesh' },
      { name: 'Rajahmundry', coordinates: [17.6868, 81.9834], description: 'City in Andhra Pradesh' },
      { name: 'Tirupati', coordinates: [13.6288, 79.4192], description: 'City in Andhra Pradesh' },
      { name: 'Vijayawada', coordinates: [16.5062, 80.6480], description: 'City in Andhra Pradesh' },
      { name: 'Visakhapatnam', coordinates: [17.6868, 83.2185], description: 'City in Andhra Pradesh' },
      { name: 'Vizianagaram', coordinates: [18.1067, 83.3956], description: 'City in Andhra Pradesh' },
     
    ],
      displayDetails: false,
      selectedLocation: null,
    };
  },
  methods: {
    showDetails(location) {
      this.displayDetails = true;
      this.selectedLocation = location;
    },
    hideDetails() {
      this.displayDetails = false;
      this.selectedLocation = null;
    },
  },
};
</script>

<style>
#map-container {
  height: 600px; 
}

.location-details {
  position: absolute;
  top: 10px;
  left: 10px;
  background-color: white;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  z-index: 1000;
}
</style>
