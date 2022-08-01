<template>
  <div class="caja" v-for="(item, index) in coincidenciaAlimento" :key="index">
    <p>{{ item.Alimento }}</p>
    <div class="description">
      Grupo de {{ item.Categoría }} - {{ item.EnergíaKcal * numPorcion }}kcal -

      {{ (item.Proteína * numPorcion).toFixed(2) }}g de proteína - {{ (item.Lípidos * numPorcion).toFixed(2) }} g de lípidos -
      {{ (item.Carbohidratos * numPorcion).toFixed(2) }}g de carbohidratos - porción: {{ (item.PesoNetoG * numPorcion).toFixed(2) }}g
    </div>

    <button @click="addFood(item, numPorcion)">Agregar</button>
  </div>
</template>

<script>
export default {
  emits: ['saved-food'],
  data() {
    return {
      foodSelected: [],
    };
  },
  methods: {
    addFood(item, numPorcion) {
      this.$emit('saved-food', item, numPorcion);
    },
  },
  props: {
    coincidenciaAlimento: {
      type: Array,
      default: () => {},
    },
    numPorcion: {
      type: Number,
      default: 1,
    },
  },
};
</script>

<style scoped>
.caja {
  /* display: grid;
  grid-template-rows: auto auto auto auto; */
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  background: #39c2e4;
  margin: 5px 5px;
  border-radius: 10px;
}
.description {
  padding: 1rem;
}
p {
  font-size: 1.2rem;
  font-weight: bold;
  text-align: center;
}

button {
  text-align: center;
  background: #333;
  border-radius: 20px;
  padding: 0.3rem;
  margin: 1rem;
}

button:hover {
  background-color: #ff00cc;
  color: white;
}
</style>
