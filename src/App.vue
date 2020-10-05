<template>
  <div id="app">
    
    <Formulario/>
  </div>
</template>

<script>
import Formulario from './components/Formulario.vue'

export default {
  name: 'App',
  components: {
    Formulario
  }
}
</script>

<style>
#app {
  margin-top: 10px;
  padding: 10px 50px;
}
</style>
