<template>
  <div id="app">
    <formulario />
  </div>
</template>

<script>
import Formulario from "./components/Formulario.vue";

export default {
  name: "App",
  components: {
    Formulario,
  },
};
</script>

<style>
#app {
  width: 80%;
  margin: 2rem 10%;
}
</style>
