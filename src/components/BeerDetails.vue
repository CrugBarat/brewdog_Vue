<template lang="html">
  <div class="details-container">
    <div class="details">
      <img :src="beer.image_url">
      <p class="name">{{beer.name}}</p>
      <p class="abv">ABV {{beer.abv}}%</p>
      <p class="description">{{beer.description}}</p>
      <beer-ingredients :beer="beer"></beer-ingredients>
    </div>
  </div>
</template>

<script>

import BeerIngredients from './BeerIngredients.vue';

export default {
  name: 'beer-detail',
  props: ['beer'],
  components: {
    "beer-ingredients": BeerIngredients
  }
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
}



</style>
