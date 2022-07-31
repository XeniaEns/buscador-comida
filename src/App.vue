<script setup>
import Title from './components/Title.vue';
import SearchFood from './components/SearchFood.vue';
</script>

<template>
  <Title titulo="Buscador de Alimentos SMAE" />
  <SearchFood />

  <footer>
    <h4 class="text-xl">Xenia Padilla, &copy;2022</h4>
  </footer>
</template>

<script>
export default {
  name: 'App',
  components: {
    Title,
    SearchFood,
  },
};
</script>

<style>
body {
  box-sizing: border-box;
  background-color: #00132d;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}

footer {
  padding: 3rem;
  margin-top: 20px;
  width: 100%;
}
</style>
