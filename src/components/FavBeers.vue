<template lang="html">
  <div>
    <p class="fav-beers">Favourite Beers</p>
    <div class="grid-list-container">
      <div class="grid-container">
        <div class="grid">
          <div v-for="beer in favBeers" v-model="favBeer=beer">
            <div class="beer-list-container">
              <div class="beer-img">
                <img class="beer-logo" :src="beer.image_url" alt="">
              </div>
              <div class="beer-name">
                <p>{{beer.name}}</p>
                <input class="remove" type="image" :src="remove" v-on:click="removeFav">
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import remove from '../assets/remove.png';
import {eventBus} from '../main.js';

export default {
  name: 'fav-beers',
  props: ['favBeers'],
  data () {
    return {
      remove: remove,
      favBeer: null
    }
  },
  methods: {
    removeFav() {
      eventBus.$emit('remove-from-favs', this.favBeer)
    }
  },
}
</script>

<style lang="css" scoped>

.fav-beers {
  font-family: 'Veneer';
  font-size: 50px;
  padding-top: 40px;
}

.grid-list-container {
  margin-left: 40px;
  margin-right: 20px;
}

.grid {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  padding: 40px;
  text-align: center;
}

.beer-list-container:hover {
  background-color: #89cff0;
  border-radius: 10%;
}

.beer-img {
  padding-top: 10px;
}

.beer-logo {
  height: 100px;
}

.beer-name {
  font-family: 'Veneer';
  font-size: 30px;
  width: 200px;
  padding-top: 10px;
}

p {
  padding: 0;
  margin: 0;
}

.remove {
  height: 30px;
}

.remove:hover {
  background-color: #89cff0;
}

.remove:focus {
  outline: none;
}


</style>
