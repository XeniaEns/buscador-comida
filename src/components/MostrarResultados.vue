<template>
  <h1>Coincidencias de alimentos</h1>

  <div class="container">
    <div class="caja" v-for="(item, index) in alimento" :key="index">
      <div class="caja titulo">
        <p>{{ item.Alimento }} [{{ item.EnergíaKcal }}kcal]</p>
        <p>Grupo de {{ item.Categoría }}</p>
      </div>
      <div class="caja proteina">
        <h5>Proteina</h5>
        <p>{{ item.Proteína }}g</p>
      </div>
      <div class="caja lipidos">
        <h5>Lípidos</h5>
        <p>{{ item.Lípidos }} kcal</p>
      </div>
      <div class="caja carbohidratos">
        <h5>Carbohidratos</h5>
        <p>{{ item.Carbohidratos }} kcal</p>
      </div>
      <div class="caja cantidad">
        <h5>Porción</h5>
        <p>{{ item.Cantidad }} {{ item.Unidad }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    alimento: {
      type: Array,
      default: () => {},
    },
  },
};
</script>

<style scoped>
.container {
  display: grid;
  grid-template-columns: auto;
  padding: 1rem;
  margin: auto;
  background-color: #cdb4db;
  border-radius: 0.5rem;
  color: rgb(33, 33, 33);
}
.caja {
  display: grid;
  grid-template-rows: auto auto auto auto;
  border: 1px solid black;
}

.titulo {
  grid-column: 1/5;
  background-color: #a2d2ff;
}
.proteina {
  background-color: #0aff99;
  grid-column: 1/2;
}
.lipidos {
  grid-column: 2/3;
  background-color: #0aefff;
}
.carbohidratos {
  grid-column: 3/4;
  background-color: #ffd300;
}
.cantidad {
  grid-column: 4/5;
  background-color: #deff0a;
}

p {
  font-size: 1.2rem;
  font-weight: bold;
  text-align: center;
}
</style>
