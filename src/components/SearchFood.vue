<script setup>
import MostrarResultados from './MostrarResultados.vue';
import MostrarListaAlimentos from './MostrarListaAlimentos.vue';
</script>

<template>
  <div class="container">
    <form @submit.prevent="">
      <label for="">Buscar Alimento</label>
      <input type="text" v-on:input="setAlimento" placeholder="Escribe el nombre del alimento" />
      <label for="">Número de porciones</label>
      <input type="number" v-on:input="setPorcion" name="portion" />
      <button @click="buscardorAlimentos">Buscar Alimento</button>
      <button @click="limpiarDatos">Limpiar datos</button>
    </form>
    <div class="boxResultados" v-if="resultadoAlimentos.length !== 0">
      <MostrarResultados :coincidenciaAlimento="resultadoAlimentos" :numPorcion="porcion" @saved-food="createFoodSelectedList" />
    </div>
  </div>

  <div class="lista-alimentos">
    <MostrarListaAlimentos :items="foodList" />
  </div>
</template>

<script>
export default {
  components: {
    MostrarResultados,
    MostrarListaAlimentos,
  },
  data() {
    return {
      alimento: '',
      porcion: 1,
      listadoAlimentos: [],
      resultadoAlimentos: [],
      foodList: [],
      activePorcion: true,
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
    createFoodSelectedList(item, cantidadItem) {
      this.foodList.push({ item, cantidadItem });
    },
    limpiarDatos() {
      this.alimento = '';
      this.resultadoAlimentos = [];
    },
    setAlimento(event) {
      this.alimento = event.target.value;
    },
    setPorcion(event) {
      this.porcion = event.target.value;
    },
    buscardorAlimentos() {
      if (this.resultadoAlimentos.length !== 0) {
        this.resultadoAlimentos = [];
      }
      this.listadoAlimentos.map((value) => {
        const foodName = value.Alimento.toLowerCase();
        if (foodName.match(`(${this.alimento.toLowerCase().trim()})`) && this.alimento !== '') {
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
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  column-gap: 20px;
  padding: 2rem;
  margin: 0 auto;
  border-radius: 10px;
  background-color: #e439c2;
}

.container form {
  display: flex;
  flex-direction: column;
  border: 1px white solid;
  padding: 1rem;
  border-radius: 5px;
}

.container input {
  margin-bottom: 20px;
  padding: 5px 0;
  text-align: center;
  color: #333;
}

input[name='portion'] {
  /* pointer-events: none; */
}

.container button {
  background: #39c2e4;
  margin: 0.5rem 0;
  padding: 5px 0;
}

.container .boxResultados {
  margin-top: 1rem;
  height: 350px;
  overflow-y: scroll;
  scroll-behavior: smooth;
}

button {
  font-weight: bold;
  border-radius: 5px;
}

.lista-alimentos {
  margin-top: 20px;
  text-align: center;
  padding: 1rem;
  background: #333;
}

.lista-alimentos table {
  display: flex;
  justify-content: center;
}

/* AGREGAR LOS MEDIA QUERY A 800PX */
@media (max-width: 800px) {
  .container {
    grid-template-columns: repeat(2, 1fr);
    column-gap: 20px;
  }
  .container form {
    padding: 1rem;
  }
  .boxResultados {
    margin: auto;
  }
}

/* AGREMAR MEDIA QUERY A 500PX */
@media (max-width: 600px) {
  .container {
    grid-template-columns: 1fr;
  }

  .container form {
    border: 1px white solid;
  }

  .boxResultados {
    padding: 0.5rem;
    border: 1px white solid;
  }
}
</style>
