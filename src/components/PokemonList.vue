<template>

  <div class="container is-max-widescreen">
    <div class="list columns is-mobile is-desktop is-multiline">
      <article class="column pr-0 is-4 is-4-mobile" v-for="(pokemon, index) in pokemons" :key="'poke'+index">
        <div class="p-2 has-background-link-dark has-text-white">
          <img :src="imageUrl + pokemon.id + '.png'" width="96" height="96" alt="">
          <h3>{{ pokemon.name }}</h3>
        </div>
      </article>
    </div>
  </div>

</template>

<script>
 export default {
    props: ['imageUrl', 'apiUrl'],
    data(){
     return {
       pokemons: [],
       nextUrl: ''
     }
   },
   created() {
     this.fetchData()
   },
   methods: {
     fetchData() {
        return this.$http.get(this.apiUrl)
          .then( (resp) => {
            this.nextUrl = resp.data.next;
            resp.data.results.forEach(pokemon => {
              pokemon.id = pokemon.url.split('/')
                .filter( part => {
                  return !!part
                }).pop();
              this.pokemons.push(pokemon)
            });
            console.log(resp.data, resp.data.next);
          })
     }
   }
  }
</script>

<style lang="scss" scoped>
  .list {

    article {
      text-align: center;
      text-transform: capitalize;
      cursor: pointer;
      
      div {
        border-radius: 5px;
        box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
      }
    }
  }
</style>