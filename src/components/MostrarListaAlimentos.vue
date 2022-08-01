<template>
  <h1>Lista de Alimentos</h1>
  <div class="grid">
    <div class="label option-1">Alimento</div>
    <div class="label option-2">Energía</div>
    <div class="label option-3">Porción</div>
    <div class="label option-4">Proteína</div>
    <div class="label option-5">Lípidos</div>
    <div class="label option-6">Carbohidratos</div>
  </div>
  <div class="grid" v-for="(item, index) in items" :key="index">
    <div class="item-properties option-1">{{ item.item.Alimento }}</div>
    <div class="item-properties option-2">{{ item.item.EnergíaKcal * item.cantidadItem }} kcal</div>
    <div class="item-properties option-3">{{ item.item.Cantidad * item.cantidadItem }} {{ item.item.Unidad }} o {{ item.item.PesoNetoG }}g</div>
    <div class="item-properties option-4">{{ item.item.Proteína * item.cantidadItem }}g</div>
    <div class="item-properties option-5">{{ item.item.Lípidos * item.cantidadItem }}g</div>
    <div class="item-properties option-6">{{ item.item.Carbohidratos * item.cantidadItem }}g</div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
    },
  },
};
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
}

.item-properties,
.label {
  padding: 0.5rem;
  border: 1px solid white;
}

@media (max-width: 600px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
  .option-4,
  .option-5,
  .option-6 {
    display: none;
  }
}
</style>
