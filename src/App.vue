<template lang="html">
 <div>
   <h1>Brewdog Beers</h1>
   <div class="main-container">
     <beer-list :beers='beers'></beer-list>
     <beer-detail v-if='selectedBeer' :beer='selectedBeer'></beer-detail>
     <button v-on:click='addFavorite'>Add Favorite</button>
     <button v-if='favoriteBeers.includes(selectedBeer)'>Delete Favorite</button>
      <div class='favorite-beers-list'>
        <h2>Favorite Beers</h2>
        <beer-list :beers='favoriteBeers'></beer-list>
      </div>
   </div>
 </div>
</template>

<script>
import BeerList from './components/BeerList.vue';
import {eventBus} from './main.js';
import BeerDetail from './components/BeerDetail.vue';


export default {
  name: 'app',
  data() {
    return {
      beers: [],
      selectedBeer: null,
      favoriteBeers: []
    };
  },

  mounted (){
    fetch('https://api.punkapi.com/v2/beers')
    .then(result => result.json())
    .then(beers => this.beers = beers)

    eventBus.$on('beer-selected', (beer) => {
      this.selectedBeer = beer
    })
  },
  methods: {
    addFavorite: function() {
      if (this.favoriteBeers.includes(this.selectedBeer) === false) {
        this.favoriteBeers.push(this.selectedBeer);
      }
    }
  },
  components: {
    'beer-list': BeerList,
    'beer-detail': BeerDetail,
  }
}
</script>

<style lang="css" scoped>
</style>
