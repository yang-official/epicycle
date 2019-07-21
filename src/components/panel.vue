<template>
  <div class="bike-panel" v-if="selectedBike">
    <div class="bike-info">
      <h3>{{ selectedBike.name }}</h3>
      <p>{{ selectedBike.priceCurrency }}{{ selectedBike.price }} per {{ selectedBike.interval }}</p>
      <button onclick="window.location.href='smartcar.html'">Book now</button>
      <button onclick="window.location.href='smartcar.html'">Unlock now</button>
    </div>
    <div class="bike-banner" v-bind:style="{ backgroundImage: `url(${selectedBike.imageUrl})` }"></div>
    <!--<div class="bike-map" v-bind:style="{ backgroundImage: `url(${mapUrl})`}"></div>-->
    <HereMap
      v-bind:selectedBike="selectedBike"
      appId="xj9v65pmNOxfqzHPSkUK"
      appCode="wp_RYYOngqNGufF4IMKF6A"
      :lat="this.selectedBike.lat"
      :lng="this.selectedBike.lng"></HereMap>
  </div>
</template>

<script>
import HereMap from './HereMap.vue'
export default {
  props: [ 'selectedBike' ],
  components: { HereMap },
  computed: {
    mapUrl: function(){
      return `http://maps.googleapis.com/maps/api/staticmap?center=${this.selectedBike.lat},${this.selectedBike.lng}&zoom=14&size=480x250&markers=${this.selectedBike.lat},${this.selectedBike.lng}&key=AIzaSyCP18cD4FwL37eXgcB1MbLNtG9ktbkzdlw`
    }
  }
};
</script>

<style scoped>
.bike-panel {
  margin: 10px;
  background-color: #98FB98;
  border-radius: 3px;
  padding: 10px;
}

.bike-banner {
  height: 250px;
  background-size: cover;
  background-position: center;
  margin-bottom: 15px;
}

.bike-map {
  height: 250px;
  background-size: cover;
  background-position: center;
}

.bike-info {
  padding: 10px;
  background-color: #ddd;
  margin-bottom: 15px;
}

.bike-info button {
  color: white;
  padding: 8px;
  font-size: 18px;
  cursor: pointer;
  background-color: #228B22;
  width: 100%;
}
</style>
