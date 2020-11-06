<template>

  <div class="container is-max-widescreen">
    <div class="list columns is-mobile is-desktop is-multiline">
      <article class="column is-4-desktop is-6-mobile is-4-tablet" v-for="(pokemon, index) in pokemons" :key="'poke'+index" @click="setPokemonUrl(pokemon.url)">
        <div class="p-2 has-background-link-dark has-text-white">
          <img :src="imageUrl + pokemon.id + '.png'" width="96" height="96" alt="">
          <h3>{{ pokemon.name }}</h3>
        </div>
      </article>

      <div id="scroll-triger" ref="infinitescrolltrigger">
        <i class="fas fa-spinner fa-spin"></i>
      </div>

    </div>
  </div>

</template>

<script>
 export default {
    props: ['imageUrl', 'apiUrl'],
    data(){
     return {
       pokemons: [],
       nextUrl: '',
       currentUrl: ''
     }
   },
   methods: {
     fetchData() {
        return this.$http.get(this.currentUrl)
          .then( (resp) => {
            this.nextUrl = resp.data.next;
            resp.data.results.forEach(pokemon => {
              pokemon.id = pokemon.url.split('/')
                .filter( part => {
                  return !!part
                }).pop();
              this.pokemons.push(pokemon)
            });

            console.log(this.nextUrl, resp.data.results);
          })
     },
     scrollTrigger() {
       const observer = new IntersectionObserver( entries => {
         entries.forEach( entry => {
           if(entry.intersectionRatio > 0 && this.nextUrl) {
             this.next()
           }
         })
       })

       observer.observe(this.$refs.infinitescrolltrigger);
     },
     next() {
       this.currentUrl = this.nextUrl;
       this.fetchData();
     },
     setPokemonUrl(url){
       this.$emit('setPokemonUrl', url);
     }
   },
   created() {
     this.currentUrl = this.apiUrl;
     this.fetchData();
   },
   mounted() {
     this.scrollTrigger();
   }
  }
</script>

<style lang="scss" scoped>
  .list {
    margin-left: 0; 
    margin-right: 0; 
    margin-top: 0;

    article {
      text-align: center;
      text-transform: capitalize;
      cursor: pointer;

      
      div {
        border-radius: 5px;
        box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);

        h3 {
          margin: 0;
        }
      }

    }

    #scroll-triger {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 150px;
      font-size: 2rem;
    }
  }
</style>