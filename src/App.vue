<template lang="html">
  <div>
    <h1> BrewD<img class="logo" src="./assets/logo.png">g</h1>
    <beer-list :beers="beers" v-model="selectedBeer"></beer-list>
    <beer-details v-if="selectedBeer" :beer="selectedBeer"></beer-details>
    <beer-ingredients v-if="beerIngredients" :beerIngredients="beerIngredients"></beer-ingredients>
    <fav-beers v-if="favBeers.length" :favBeers="favBeers"></fav-beers>
  </div>
</template>


<script>

import BeerList from './components/BeerList.vue';
import BeerDetails from './components/BeerDetails.vue';
import BeerIngredients from './components/BeerIngredients.vue';
import FavBeers from './components/FavBeers.vue';

import {eventBus} from './main.js'

export default {
  name: 'app',
  data () {
    return {
      beers: [],
      selectedBeer: null,
      beerIngredients: null,
      favBeers: [],
      searchBeers: ""
    }
  },
  components: {
    "beer-list": BeerList,
    "beer-details": BeerDetails,
    "beer-ingredients": BeerIngredients,
    "fav-beers": FavBeers
  },
  methods: {
    addtoFavs(beer) {
      if (!this.favBeers.includes(beer)) {
          this.favBeers.push(beer)
      } else {
        alert('Beer already added! Try another!')
      }
    },
    removeFav(beer) {
      if (this.favBeers.includes(beer)) {
        const index = this.favBeers.indexOf(beer)
        return this.favBeers.splice(index, 1)
    } else {
      alert('This beer is not one of your favourites!')
    }
  },
},
  mounted() {
    fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
    .then(res => res.json())
    .then(beers => this.beers = beers)

    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer;
      this.searchBeers = ""
    });

    eventBus.$on('search-beers', (searchBeers) => {
      this.searchBeers = searchBeers;
      this.beerIngredients = null;
    });

    eventBus.$on('beer-ingredients', (beer) => {
      this.beerIngredients = beer;
      this.selectedBeer = null;
    });

    eventBus.$on('add-to-favs', (beer) => {
      this.addtoFavs(beer);
    });

    eventBus.$on('remove-from-favs', beer => this.removeFav(beer));
  }
}
</script>


<style lang="css" scoped>

h1 {
  font-family: 'Veneer';
  font-size: 170px;
  text-align: center;
  margin: 0;
  padding: 0;
  color: 	#202020;
  opacity: 80%;
}

.logo{
  height: 130px;
  padding: 0;
  margin: 0;
}
</style>

<style>
body {
  background-image: url('./assets/background1.png');
  background-position: center;
  background-attachment: fixed;
  background-size: cover;
  width: 100vw;
  font-family: 'Roboto', monospace;
  display: block;
  text-align: center;
  cursor: url('./assets/beer.png'), auto;
  user-select: none;
}

@font-face {
  font-family: 'Veneer';
  src: url('./assets/fonts/VeneerTwo.ttf');
}
</style>
