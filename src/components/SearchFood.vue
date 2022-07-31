<script setup>
import MostrarResultados from './MostrarResultados.vue';
</script>

<template>
  <div class="container">
    <label for="">Buscar Alimento</label>
    <input type="search" v-model="alimento" @keyup.enter="buscardorAlimentos" />
    <button @click="buscardorAlimentos">Buscar Alimento</button>
  </div>
  <div v-if="resultadoAlimentos.length !== 0">
    <MostrarResultados :coincidenciaAlimento="resultadoAlimentos" />
  </div>
</template>

<script>
export default {
  components: {
    MostrarResultados,
  },
  data() {
    return {
      alimento: '',
      listadoAlimentos: [],
      resultadoAlimentos: [],
    };
  },
  created() {
    if (localStorage.getItem('dbalimentos') !== null) {
      this.listadoAlimentos = JSON.parse(localStorage.getItem('dbalimentos'));
    } else {
      this.listaComida();
    }
  },
  methods: {
    buscardorAlimentos() {
      if (this.resultadoAlimentos.length !== 0) {
        this.resultadoAlimentos = [];
      }
      this.listadoAlimentos.map((value) => {
        const foodName = value.Alimento.toLowerCase();
        if (foodName.match(`(${this.alimento.toLowerCase().trim()})`) && this.alimento.trim() !== '') {
          this.resultadoAlimentos.push(value);
        }
      });
    },
    listaComida: async function () {
      const respuesta = await fetch('https://primer-rest-api-bf3e4-default-rtdb.firebaseio.com/SMAE.json');
      const data = await respuesta.json();
      this.listadoAlimentos = data;
      this.revisarLocalStorage();
    },
    revisarLocalStorage() {
      localStorage.setItem('dbalimentos', JSON.stringify(this.listadoAlimentos));
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  margin: auto;
  padding: 2rem;
  background-color: #00132daf;
}
label {
  margin-bottom: 0.5rem;
}

input {
  padding: 1rem;
  border-radius: 0.5rem;
  text-align: center;
  color: #333;
}

button {
  outline: none;
  margin: 1rem 0;
  padding: 0.5rem;
  background-color: #ffafcc;
  color: white;
  font-weight: bold;
  font-size: 1.5rem;
  border-radius: 10px;
}
</style>
