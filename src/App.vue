<template lang="html">
  <div>
    <h1>Beers</h1>
    <beer-list :beers="beers" v-model="selectedBeer"></beer-list>
  </div>
</template>


<script>

import BeerList from './components/BeerList.vue';

import {eventBus} from './main.js'

export default {
  name: 'app',
  data () {
    return {
      beers: [],
      selectedBeer: null
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
    "beer-list": BeerList
  }
}
</script>


<style lang="css" scoped>
</style>
