<template>
  <div class="main-container">
    <h2>Adicione Livros</h2>
    <FormBooks/>
  </div>
</template>

<script>
  import FormBooks from '../components/FormBooks.vue'
  export default {
    name: 'AddLivros',

    components: {
      FormBooks
    }
  }
</script>

<style scoped>
  h2 {
    text-align: center;
    margin-bottom: 3%;
    margin-left: -12%;
  }
</style>
