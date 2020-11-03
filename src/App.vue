<template>
  <div id="app">
    <Pokemon></Pokemon>
  </div>
</template>

<script>
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  components: {
    Pokemon
  }
}
</script>

<style>
  *, ::before, ::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  a {
    text-decoration: none;
    outline: none;
  }

  ul, li {
    list-style: none;
  }
  
#app {
  color: #2c3e50;
}
</style>
