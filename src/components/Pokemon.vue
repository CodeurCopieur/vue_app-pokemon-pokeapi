<template>
 <div class="container">
   <h1 class="title has-text-centered block">Pokemon's</h1>

   <PokemonSearch></PokemonSearch>
   <PokemonList :imageUrl="imageUrl" :apiUrl="apiUrl" @setPokemonUrl="setPokemonUrl"></PokemonList>
   <PokemonDetail v-if="showDetail" :pokemonUrl="pokemonUrl" :imageUrl="imageUrl" @closeDetail="closeDetail"></PokemonDetail>
 </div>
</template>

<script>
import PokemonSearch from './PokemonSearch'
import PokemonList from './PokemonList'
import PokemonDetail from './PokemonDetail'

 export default {
   data() {
     return {
      imageUrl: 'https://pokeres.bastionbot.org/images/pokemon/',
      apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
      pokemonUrl: '',
      showDetail: false
     }
   },
   components: {
     PokemonSearch,
     PokemonList,
     PokemonDetail
   },
   methods: {
     setPokemonUrl(url) {
       this.pokemonUrl = url;
       this.showDetail = true;
     },
     closeDetail(){
       this.pokemonUrl = '';
       this.showDetail = false;
     }
   }
  }
</script>

<style lang="scss" scoped>
  @import url('https://use.fontawesome.com/releases/v5.8.2/css/all.css');
</style>