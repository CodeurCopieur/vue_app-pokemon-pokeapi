<template>
  <div class="searchBar column is-offset-one-quarter mb-4">
    <div class="control is-vcentered">
      <form @submit.prevent="setPokemonUrl">
        <input type="text" class="input is-info is-rounded" v-model="searchValue">
      </form>
      <i class="fas fa-search" @click="setPokemonUrl"></i>
    </div>
  </div>

</template>

<script>
 export default {
   props: ['apiUrl'],
   data() {
     return {
       searchValue: ''
     }
   },
   methods: {
     setPokemonUrl() {

       console.log(this.apiUrl + this.searchValue.toLowerCase());
       if(this.searchValue !== '') {
         this.$emit('setPokemonUrl', this.apiUrl + this.searchValue.toLowerCase())
       }
         
     }
   }
  }
</script>

<style lang="scss" scoped>
  .searchBar {
    position: relative;
    width: 100%;
    max-width: 510px;

    i {
      position: absolute;
      top: 10px;
      right: 10px;
      font-size: 1.25rem;
      color:#2160c4;
      cursor: pointer;
    }
  }
</style>