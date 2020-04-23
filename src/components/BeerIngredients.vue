<template lang="html">
  <div class="">
  <div v-for="ingredient in beer.ingredients">
    <p v-for="oneIngredient in ingredient">{{oneIngredient.name}}</p>
    <p>{{beer.ingredients.yeast}}</p>
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
