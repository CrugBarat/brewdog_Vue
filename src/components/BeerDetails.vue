<template lang="html">
  <div class="">
    <img :src="beer.image_url">
    <p>{{beer.name}}</p>
    <p>{{beer.description}}</p>
    <p>{{beer.abv}}</p>
  </div>
</template>

<script>

export default {
  name: 'beer-detail',
  props: ['beer'],
  data () {
    return {
      favBeers: []
    }
  },
}
</script>

<style lang="css" scoped>

img {
  height: 100px;
}

</style>
