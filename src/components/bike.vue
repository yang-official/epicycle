<template>
  <div class="bike" v-on:click="handleClick">
    <div class="bike-picture" v-bind:style="{ backgroundImage: `url(${bikeInfo.imageUrl})` }"></div>
    <div class="bike-title">
      {{ title }}
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    title: function() {
      return `${this.bikeInfo.priceCurrency}${this.bikeInfo.price}/${this.bikeInfo.interval} - ${this.bikeInfo.name}`
    }
  },
  props: ['bikeInfo'],
  methods: {
    handleClick: function(){
      this.$emit('selectedBikeChanged', this.bikeInfo)
    }
  }
}
</script>

<style scoped>
.bike {
  flex-basis: calc(50% - 20px);
  margin: 10px;
  cursor: pointer;
}

.bike:hover {
  opacity: 0.8;
}

.bike-picture {
  height: 200px;
  background-size: cover;
  background-position: center;
}

.bike-title {
  margin-top: 10px;
  font-weight: bold;
}
</style>
