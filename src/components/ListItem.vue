<template lang="html">
  <li v-on:click="handleClick">{{beer.name}}</li>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'list-item',
  props: ['beer'],
  methods: {
    handleClick() {
      eventBus.$emit('selected-beer', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>

li {
  list-style-type: none;
  font-size: 20px;
  text-shadow: -1px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000, 1px 1px 0 #000;
}
</style>
