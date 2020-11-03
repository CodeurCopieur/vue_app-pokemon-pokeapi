<template>
 <div>
   <h1 class="title has-text-centered">Pokemon's</h1>

   <PokemonSearch></PokemonSearch>
   <PokemonList :imageUrl="imageUrl" :apiUrl="apiUrl"></PokemonList>
   <PokemonDetail></PokemonDetail>
 </div>
</template>

<script>
import PokemonSearch from './PokemonSearch'
import PokemonList from './PokemonList'
import PokemonDetail from './PokemonDetail'

 export default {
   data() {
     return {
       imageUrl: 'https://pokeres.bastionbot.org/images/pokemon/1.png',
        apiUrl: 'https://pokeapi.co/api/v2/pokemon/'
     }
   },
   components: {
     PokemonSearch,
     PokemonList,
     PokemonDetail
   },
   methods: {

   }
  }
</script>

<style lang="scss" scoped>


</style>