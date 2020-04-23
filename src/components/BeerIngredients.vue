<template lang="html">
  <div class="ingredients">
    <span>{{beerIngredients}}</span>
  </div>


</template>

<script>
export default {
  name: 'beer-ingredients',
  props: ['beerIngredients']
}
</script>

<style lang="css" scoped>

.ingredients:hover {

}
</style>
