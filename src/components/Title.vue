<template>
  <h1 class="text-3xl m-1">{{ titulo }}</h1>
  <h5>@xenianutrition</h5>
  <hr />
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
hr {
  margin: 0 10%;
}
</style>
