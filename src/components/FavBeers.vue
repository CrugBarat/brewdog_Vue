<template lang="html">
  <div>
    <p>Fav Beers</p>
    <div v-for="beer in favBeers">
      <p>{{beer.name}} - <span>{{beer.tagline}}</span></p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'fav-beers',
  props: ['favBeers']
}
</script>

<style lang="css" scoped>
</style>
