<script setup>
import Title from './components/Title.vue';
import SearchFood from './components/SearchFood.vue';
</script>

<template>
  <Title titulo="Buscador de Alimentos SMAE" />
  <SearchFood />
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
  background-color: #39c2e4;
  color: #ffffff;
}
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
} */
</style>
