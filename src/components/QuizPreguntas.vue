<template>
  <div class="card">
    <div class="card-header">
      <h2 class="mb-0">Preguntas y Respuestas</h2>
    </div>
    <div class="card-body">
      <div v-for="(pregunta, index) in preguntas" :key="index" class="mb-4">
        <h5 class="mb-3">Pregunta {{ index + 1 }}/5</h5>
        <p class="fw-bold">{{ pregunta.pregunta }}</p>
        <div class="list-group">
          <div
            v-for="(opcion, opcionIndex) in pregunta.opciones"
            :key="opcionIndex"
            class="list-group-item"
            :class="{
              'list-group-item-success': opcion.esCorrecta,
              'list-group-item-danger': pregunta.respuestaSeleccionada === opcionIndex && !opcion.esCorrecta
            }"
          >
            <div class="form-check">
              <input
                :id="`p${index}-o${opcionIndex}`"
                v-model="pregunta.respuestaSeleccionada"
                type="radio"
                :name="`pregunta-${index}`"
                :value="opcionIndex"
                class="form-check-input"
              />
              <label :for="`p${index}-o${opcionIndex}`" class="form-check-label">
                {{ opcion.texto }}
              </label>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'QuizPreguntas',
  data() {
    return {
      preguntas: [
        {
          pregunta: 'Cual es la forma correcta de registrar el evento de click en VueJS?',
          opciones: [
            { texto: 'a) v-on@click', esCorrecta: false },
            { texto: 'b) #click', esCorrecta: false },
            { texto: 'c) @click', esCorrecta: true },
            { texto: 'd) :click', esCorrecta: false },
            { texto: 'e) v-bind#click', esCorrecta: false },
            { texto: 'f) v-on:click', esCorrecta: true }
          ],
          respuestaSeleccionada: null
        },
        {
          pregunta: 'npm create vue@latest se utiliza para:',
          opciones: [
            { texto: 'a) Crear un componente Vue', esCorrecta: false },
            { texto: 'b) Crear un aplicación Vue', esCorrecta: true },
            { texto: 'c) Instalar Pinia', esCorrecta: false },
            { texto: 'd) Instalar una dependencia', esCorrecta: false }
          ],
          respuestaSeleccionada: null
        },
        {
          pregunta: 'El modificador trim recorta...',
          opciones: [
            { texto: 'a) Los espacios puestos adelante en una entrada de texto', esCorrecta: false },
            { texto: 'b) Los espacios puestos atrás en una entrada de texto', esCorrecta: false },
            { texto: 'c) Los espacios adelante y atrás en una entrada de texto', esCorrecta: true },
            { texto: 'd) Saca los espacios intermedios puestos en una entrada de texto', esCorrecta: false }
          ],
          respuestaSeleccionada: null
        },
        {
          pregunta: 'La propiedad routes en la definición del router de Vue.js tiene como función:',
          opciones: [
            { texto: 'a) Definir el path y el componente activo para esa ruta', esCorrecta: true },
            { texto: 'b) Define la barra de navegación a utilizar', esCorrecta: false },
            { texto: 'c) Define sólo todos los componentes activos en el router', esCorrecta: false },
            { texto: 'd) Definir el modo de trabajo de las rutas', esCorrecta: false }
          ],
          respuestaSeleccionada: null
        },
        {
          pregunta: 'Las actions en Pinia contienen...',
          opciones: [
            { texto: 'a) Módulos de Pinia', esCorrecta: false },
            { texto: 'b) La lógica para cambiar el estado global de la aplicación', esCorrecta: true },
            { texto: 'c) El estado global', esCorrecta: false },
            { texto: 'd) Getters', esCorrecta: false }
          ],
          respuestaSeleccionada: null
        }
      ]
    }
  }
}
</script>

<style scoped>
.card {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.list-group-item-success {
  background-color: #d4edda;
  border-color: #c3e6cb;
}

.list-group-item-danger {
  background-color: #f8d7da;
  border-color: #f5c6cb;
}
</style>

