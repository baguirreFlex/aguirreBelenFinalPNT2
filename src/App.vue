<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-8 offset-md-2">
        <h1 class="text-center mb-4">Conversor a Dólares</h1>
        
        <ConversorMoneda />
        
        <QuizPreguntas />
      </div>
    </div>
  </div>
</template>

<script>
import ConversorMoneda from './components/ConversorMoneda.vue'
import QuizPreguntas from './components/QuizPreguntas.vue'

export default {
  name: 'App',
  components: {
    ConversorMoneda,
    QuizPreguntas
  }
}
</script>

<style scoped>
</style>

