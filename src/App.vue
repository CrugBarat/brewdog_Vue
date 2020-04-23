<template lang="html">
  <div>
    <h1>Beers</h1>
    <beer-list :beers="beers" v-model="selectedBeer"></beer-list>
    <beer-details v-if="selectedBeer" :beer="selectedBeer"></beer-details>
    <button v-if="!favBeers.includes(selectedBeer)" v-on:click="addtoFavs">Add to Fav</button>
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
    fetch('https://api.punkapi.com/v2/beers')
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
    }
  }
}
</script>


<style lang="css" scoped>
</style>
