<template>
  <div class="container">
    <div class="main">
      <div class="search">
        <input type="text" v-model="query" v-on:input="filterBikes">
      </div>
      <div class="bikes">
        <bike v-for='bike in bikes' v-bind:bikeInfo='bike' v-on:selectedBikeChanged='changedSelectedBike'></bike>
      </div>
    </div>
    <div class="panel">
      <panel v-bind:selectedBike="selectedBike"></panel>
    </div>
  </div>
</template>

<script>
import Bike from './components/bike.vue'
import Panel from './components/panel.vue'
import Entries from './data/bikes.json'

export default {
  data () {
    return {
      query: '',
      allBikes: [],
      bikes: [],
      selectedBike: null
    }
  },
  components: { Bike, Panel },
  mounted: function() {
    this.allBikes = Entries
    this.bikes = Entries
    this.selectedBike = this.bikes[0]
  },
  methods: {
    filterBikes: function(e){
      this.query = e.currentTarget.value;
      this.bikes = this.allBikes.filter((bike) => new RegExp(this.query, 'i').exec(bike.name))
    },
    changedSelectedBike: function(bike){
      this.selectedBike = bike;
    }
  },
}
</script>

<style scoped>
.container {
  display: flex;
}

.main {
  display: flex;
  flex-basis: 60%;
  flex-direction: column;
}

.search {
  padding: 10px;
}

.search input {
  width: 100%;
  height: 30px;
  font-size: 18px;
}

.bikes {
  display: flex;
  flex-wrap: wrap;
}

.panel {
  height: 100vh;
  flex-basis: 40%;
  top: 0;
  position: sticky;
}
</style>
