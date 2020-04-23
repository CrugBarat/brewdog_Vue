<template lang="html">
  <div class="">
  <div v-for="ingredient in beer.ingredients">
    <span v-for="oneIngredient in ingredient">{{oneIngredient.name}} </span>
    <span>{{beer.ingredients.yeast}}</span>
  </div>
  </div>
</template>

<script>
export default {
  name: 'beer-ingredients',
  props: ['beer']
}
</script>

<style lang="css" scoped>
</style>
