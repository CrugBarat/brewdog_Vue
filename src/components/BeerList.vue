<template lang="html">
  <div class="list-container">
    <div class="list">
      <input type="text" placeholder="Search" v-model="searchBeers">
      <list-item v-if="searchBeers" v-for="(beer, index) in filteredBeers" :beer="beer" :key="index"></list-item>
    </div>
  </div>
</template>

<script>

import ListItem from './ListItem.vue'



export default {
  name: 'beer-list',
  props:['beers'],
  data () {
    return {
      searchBeers: ""
    }
  },
  computed: {
    filteredBeers(){
      return this.beers.filter((beer) => {
        return beer.name.toLowerCase().includes(this.searchBeers.toLowerCase())
      });
    }
  },
  components: {
    'list-item': ListItem
  }
}

</script>

<style lang="css" scoped>
.list-container {
  display: block;
  text-align: center;
}

.list {
  display: inline-block;
  width: 400px;
}

input[type=text] {
  width: 400px;
  height: 20px;
  font-size: 20px;
  font-family: 'Roboto', cursive;
  border: solid 2px #fff;
  color: #fff;
  background-color: transparent;
}

::placeholder {
    color: #fff;
}

input:focus {
  outline: none;
}
</style>
