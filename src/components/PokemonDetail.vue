<template>
  <div class="detail">
    <div class="detail-view" v-if="show">
      <div v-if="pokemon" class="image">
        <img :src="imageUrl + pokemon.id + '.png'" alt="">
      </div>
    </div>
    <i v-else class="fas fa-spinner fa-spin"></i>
  </div>
</template>

<script>
 export default {
   props: ['pokemonUrl', 'imageUrl'],
   data(){
     return {
       show: false,
       pokemon: {}
     }
   },
   methods: {
     fetchData() {
       return this.$http.get(this.pokemonUrl)
          .then( (resp) => {
            this.pokemon = resp.data;
            this.show =  true;
          })
     }
   },
   created() {
     this.fetchData();
   }
  }
</script>

<style lang="scss" scoped>
  
  .detail {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: fixed;
    top: 0;
    left: 0;
    padding: 90px 10px 10px;
    width: 100%;
    height: 100vh;
    background: rgba($color: #000000, $alpha: .7);

    .detail-view {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      position: relative;
      width: 100%;
      max-width: 510px;
      padding: 50px 0 0;
      border-radius: 5px;
      background-color: #fff;
      box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
      .image {
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        top: -90px;
        width: 120px;
         padding: 10px;
        align-items: center;      
        height: 120px;
        background-color: #2160c4;
        border-radius: 50%;
        overflow: hidden;
        box-shadow: 0 15px 30px rgba(0,0,0,.2),
                  0 10px 10px rgba(0,0,0,.2);
      }
    }
  }

</style>