<template lang="html">
  <div class="">
    <img :src="beer.image_url">
    <p>{{beer.name}}</p>
    <p>{{beer.description}}</p>
    <p>{{beer.abv}}</p>
    <beer-ingredients :beer="beer"></beer-ingredients>
  </div>
</template>

<script>

import BeerIngredients from './BeerIngredients.vue';

export default {
  name: 'beer-detail',
  props: ['beer'],
  data () {
    return {
      favBeers: []
    }
  },
  components: {
    "beer-ingredients": BeerIngredients
  }
}
</script>

<style lang="css" scoped>

img {
  height: 100px;
}

</style>
