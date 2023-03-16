<template>
  <div class="main-container">
    <h2>Lista de Livros Disponiveis</h2>
    <Tablebooks/>
  </div>
</template>

<script>
import Tablebooks from '../components/Tablebooks.vue'

export default {

  name: 'Home',

  components : {
    Tablebooks
  }
}
</script>

<style scoped>
  h2 {
    text-align: center;
    margin-bottom: 3%;
  }
</style>
