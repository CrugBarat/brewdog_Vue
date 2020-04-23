<template lang="html">
  <div>
    <div class="search-container">
      <div class="search">
        <input type="text" placeholder="Search" v-model="searchBeers">
      </div>
    </div>
    <div class="grid-list-container">
      <div class="grid-container">
        <div class="grid">
          <list-item class="list" v-if="searchBeers" v-for="(beer, index) in filteredBeers" :beer="beer" :key="index"></list-item>
        </div>
      </div>
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
.search-container {
  border-style: solid;
  width: 100vw;
}

.search {
  width: 500px;
  border-style: solid;
  display: inline-block;
}

input[type=text] {
  width: 400px;
  height: 20px;
  font-size: 20px;
  font-family: 'Roboto', monospace;
  border: solid 2px #202020;
  color: 	#202020;
  background-color: transparent;
}

::placeholder {
  color: 	#202020;
}

input:focus {
  outline: none;
}

.grid-list-container {
  border-style: solid;
}

.grid-container {
  border-style: solid;
  margin-left: 20px;
  margin-right: 20px;
}

.grid {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  padding: 40px;
  text-align: center;
}

.list {
  border-radius: 5%;
  flex: 1, 0, auto;
}
</style>
