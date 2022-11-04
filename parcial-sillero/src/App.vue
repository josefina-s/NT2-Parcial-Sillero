<template>
  <div id="app">
    <h1>Parcial NT2 Josefina Sillero</h1>
    <Navbar/>
    <router-view></router-view>
  </div>
</template>

<script>

import Navbar from './componentes/Navbar.vue'
export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
