<template lang="html">
  <div>
    <h1>BrewDog</h1>
    <beer-list :beers="beers" v-model="selectedBeer"></beer-list>
    <beer-details v-if="selectedBeer" :beer="selectedBeer"></beer-details>
    <button v-if="!favBeers.includes(selectedBeer)" v-on:click="addtoFavs">Add to Fav</button>
    <button v-if="favBeers.includes(selectedBeer)" v-on:click="removeFav">Remove Fav</button>
    <fav-beers :favBeers="favBeers"></fav-beers>
  </div>
</template>


<script>

import BeerList from './components/BeerList.vue';
import BeerDetails from './components/BeerDetails.vue';
import FavBeers from './components/FavBeers.vue';

import {eventBus} from './main.js'

export default {
  name: 'app',
  data () {
    return {
      beers: [],
      selectedBeer: null,
      favBeers: []
    }
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
    .then(res => res.json())
    .then(beers => this.beers = beers)

    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer;
    });

  },
  components: {
    "beer-list": BeerList,
    "beer-details": BeerDetails,
    "fav-beers": FavBeers
  },
  methods: {
    addtoFavs() {
      this.favBeers.push(this.selectedBeer)
    },
    removeFav() {
      this.favBeers.pop(this.selectedBeer)
    }
  }
}
</script>


<style lang="css" scoped>

h1 {
  font-family: 'Girassol', cursive;
  font-size: 150px;
  text-align: center;
  margin: 0;
  padding: 0;
}
</style>

<style>
body {
  background-image: url('./assets/background.png');
  background-position: center;
  background-size: cover;
  background-repeat: repeat-y;
  width: 100vw;
  height: 100vh;
  color: #fff;
}
</style>
