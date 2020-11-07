<template>
  <div class="detail">
    <div class="detail-view" v-if="show">
      <div v-if="pokemon" class="image">
        <img :src="imageUrl + pokemon.id + '.png'" alt="">
      </div>

      <div v-if="pokemon" class="data mb-3">
        <h2> {{ pokemon.name }}</h2>

        <div class="propriete">
          <div class="left">Base Expérience</div>
          <div class="right">{{pokemon.base_experience }} XP</div>
        </div>

        <div class="propriete">
          <div class="left">Taille</div>
          <div class="right">{{pokemon.height / 10 }} m</div>
        </div>

        <div class="propriete">
          <div class="left">Poid</div>
          <div class="right">{{pokemon.weight / 10 }} kg</div>
        </div>

        <h3 class="mt-4 mb-1">Types de pokemon</h3>
        <div class="types">
          <div class="type" v-for="(value, index) in pokemon.types" :key="'value' + index">
            <span class="tag is-info">{{ value.type.name }}</span>
          </div>
        </div>
        
        <h3 class="mt-4 mb-1">Capacités</h3>
        <div class="capacites">
          <div class="capacite" v-for="(value, index) in pokemon.abilities" :key="'value' + index">
            <span class="tag is-success">{{ value.ability.name }}</span>
          </div>
        </div>
      </div>
      <div v-else >
        <h2>Le pokémon n'a pas été trouvé</h2>
      </div>
      <button class="button is-info is-rounded mb-5" @click="closeDetail">Fermer</button>
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
            this.show = true;
          })
          .catch((error) => {
            console.log(error);
          })
     },
     closeDetail() {
       this.$emit('closeDetail');
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

      .data {

        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        width: 100%;

        h2 {
          text-transform: capitalize;
          font-weight: bold;
        }

        .propriete {
          width: 90%;
          max-width: 400px;
          border-bottom: 1px solid #2160c4;
          margin-bottom: 10px;
          display: flex;
          justify-content: space-between;
        }

        h3 {
          width: 90%;
          max-width: 400px;
          font-weight: bold;
          border-bottom: 1px solid #2160c4;
        }

        .types, .capacites {
          display: flex;
          justify-content: flex-start;
          flex-wrap: wrap;
          width: 90%;
          max-width: 400px;

          .type, .capacite {
            margin: 0 10px 10px 0;
            font-weight: 600;
            font-size: 1.5rem;
            letter-spacing: 2px;
            text-transform: capitalize;
            word-wrap: none;
            word-break: keep-all;
          }
        }
      }
    }

    i {
      font-size: 2rem;
      color: #efefef;
    }
  }

</style>