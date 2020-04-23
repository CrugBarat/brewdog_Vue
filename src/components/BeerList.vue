<template lang="html">
  <div>
  <list-item v-for="(beer, index) in beers" :beer="beer" :key="index"></list-item>
  </div>
</template>

<script>

import ListItem from './ListItem.vue'

import {eventBus} from '../main.js'

export default {
  name: 'beer-list',
  props:['beers'],
  components: {
    'list-item': ListItem
  }
}

</script>

<style lang="css" scoped>
</style>
