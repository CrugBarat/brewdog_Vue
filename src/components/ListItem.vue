<template lang="html">
  <div  class="beer-list-container">
    <div class="beer-img">
      <img class="beer-logo" :src="beer.image_url" alt="">
    </div>
    <div class="beer-name">
      <p>{{beer.name}}</p>
      <p class="abv">ABV {{beer.abv}}%</p>
    </div>
    <button v-on:click="handleClick">More Info</button>
    <button v-on:click="addtoFavs">Add to Fav</button>
    <button v-on:click="removeFav">Remove Fav</button>
  </div>
</template>


<script>
import FavBeers from './FavBeers.vue';
import {eventBus} from '../main.js'

export default {
  name: 'list-item',
  data () {
    return {
      favBeers: [],
      selectedBeer: null
    }
  },
  props: ['beer'],
  methods: {
    handleClick() {
      eventBus.$emit('selected-beer', this.beer)
    },
    addtoFavs() {
      eventBus.$emit('add-to-favs', this.beer)
    },
    removeFav() {
      eventBus.$emit('remove-from-favs', this.beer)
    }
  },
  mounted() {
    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer;
    });
  },
}
</script>



<style lang="css" scoped>

.beer-list-container {
  /* border-style: solid; */
}

.beer-list-container:hover {
  background-color: #89cff0;
}

.beer-img {
  padding-top: 10px;
}

.beer-name {
  font-family: 'Veneer';
  font-size: 30px;
  width: 200px;
  padding-top: 10px;
}

.beer-logo {
  height: 100px;
}

P {
  margin: 0;
  padding: 0;
}

.abv {
  font-size: 20px;
}




</style>
