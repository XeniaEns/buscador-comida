<template>
  <div>
    <h1 class="text-3xl m-1">{{ titulo }}</h1>
    <h5>@xenianutrition</h5>
  </div>
</template>

<script>
export default {
  props: {
    titulo: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
div {
  background: #c2e439;
  padding: 20px 0;
  margin-bottom: 3rem;
  color: #333;
}

h1,
h5 {
  font-weight: bold;
  color: white;
  text-align: center;
}
</style>
