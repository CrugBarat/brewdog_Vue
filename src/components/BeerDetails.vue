<template lang="html">
  <div class="details-container">
    <div class="details">
      <img :src="beer.image_url">
      <p class="name">{{beer.name}}</p>
      <p class="abv">ABV {{beer.abv}}%</p>
      <p class="description">{{beer.description}}</p>
      <div class="buttons-container">
      <div class="buttons">
        <div class="ingreds-butn">
          <input class="ingredients" type="image" :src="ingredients" v-on:click="handleClick">
        </div>
        <div class="add-butn">
          <input class="add" type="image" :src="add" v-on:click="addtoFavs">
        </div>
        <div class="remove-butn">
          <input class="remove" type="image" :src="remove" v-on:click="removeFav">
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import {eventBus} from '../main.js';
import add from '../assets/add.png';
import remove from '../assets/remove.png';
import ingredients from '../assets/ingredients.png';

export default {
  name: 'beer-detail',
  props: ['beer'],
  data () {
    return {
      add: add,
      remove: remove,
      ingredients: ingredients,
    }
  },
  methods: {
    addtoFavs() {
      eventBus.$emit('add-to-favs', this.beer)
    },
    removeFav() {
      eventBus.$emit('remove-from-favs', this.beer)
    },
    handleClick() {
      eventBus.$emit('beer-ingredients', this.beer.ingredients)
    }
  },
}
</script>

<style lang="css" scoped>

.details-container {
  width: 100vw;
  display: block;
  text-align: center;
}

.details {
  width: 800px;
  display: inline-block;
}

img {
  height: 150px;
  padding-bottom: 10px;
}

P {
  margin: 0;
  padding: 0;
}

.name {
  font-family: 'Veneer';
  font-size: 50px;
}

.abv {
  font-family: 'Veneer';
  font-size: 30px;
}

.description {
  font-family: 'Roboto';
  font-size: 20px;
  padding-bottom: 20px;
  padding-top: 20px;
}

.ingredients {
  height: 50px;
}

.add {
  height: 50px;
}

.remove {
  height: 50px;
}

.add:hover {
  background-color: #89cff0;
  border-radius: 50%;
}

.ingredients:hover {
  background-color: #89cff0;
}

.remove:hover {
  background-color: #89cff0;
}

input:focus{
  outline: none;
}

.buttons-container {
  text-align: center;
  display: block;
}

.buttons {
  display: inline-block;
  width: 300px;
  padding-top: 10px;
}

.ingreds-butn {
  width:30%;
  float: left;
}

.add-butn {
  width:30%;
  float: left;
}

.remove-butn {
  width:30%;
  float: left;
}

</style>
