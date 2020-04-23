<template lang="html">
  <div>
    <h3>{{beer.name}} ABV:{{beer.abv}}</h3>
    <p>Description: {{beer.description}}</p>
  </div>
</template>

<script>
export default {
  name: 'beer-detail',
  props: ['beer']
}
</script>

<style lang="css" scoped>
</style>
