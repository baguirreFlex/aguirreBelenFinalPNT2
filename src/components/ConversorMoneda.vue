<template>
  <div class="card mb-4">
    <div class="card-body">
      <div class="mb-3">
        <label for="monto" class="form-label">Ingrese monto $</label>
        <input
          id="monto"
          v-model.number="monto"
          type="number"
          class="form-control"
          placeholder="Ingrese el monto en pesos"
          min="0"
          step="0.01"
        />
      </div>
      
      <div class="mb-3">
        <label for="cotizacion" class="form-label">Valor del dólar en $</label>
        <div class="input-group">
          <input
            id="cotizacion"
            v-model.number="cotizacionDolar"
            type="number"
            class="form-control"
            placeholder="Ingrese la cotización del dólar"
            min="0"
            step="0.01"
            :disabled="actualizacionAutomatica"
          />
          <div class="input-group-text">
            <input
              id="checkbox-actualizacion"
              v-model="actualizacionAutomatica"
              type="checkbox"
              class="form-check-input me-2"
            />
            <label for="checkbox-actualizacion" class="form-check-label mb-0">
              Actualización
            </label>
          </div>
        </div>
        <div v-if="actualizacionAutomatica && fechaActualizacion" class="mt-2 text-muted small" :key="timestampActualizacion">
          {{ fechaActualizacion }}
        </div>
      </div>
      
      <div class="alert alert-info">
        <strong>Valor convertido USD {{ valorConvertido.toFixed(2) }}</strong>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ConversorMoneda',
  data() {
    return {
      monto: 1000,
      cotizacionDolar: 315,
      actualizacionAutomatica: false,
      fechaActualizacion: null,
      intervaloActualizacion: null,
      timestampActualizacion: null
    }
  },
  computed: {
    valorConvertido() {
      if (this.monto && this.cotizacionDolar && this.cotizacionDolar > 0) {
        return this.monto / this.cotizacionDolar
      }
      return 0
    }
  },
  watch: {
    actualizacionAutomatica(nuevoValor) {
      if (nuevoValor) {
        this.iniciarActualizacionAutomatica()
      } else {
        this.detenerActualizacionAutomatica()
      }
    }
  },
  beforeUnmount() {
    this.detenerActualizacionAutomatica()
  },
  methods: {
    formatearFechaHora(timestamp) {
      const fecha = new Date(timestamp)
      const dia = String(fecha.getDate()).padStart(2, '0')
      const mes = String(fecha.getMonth() + 1).padStart(2, '0')
      const año = fecha.getFullYear()
      const horas = String(fecha.getHours()).padStart(2, '0')
      const minutos = String(fecha.getMinutes()).padStart(2, '0')
      const segundos = String(fecha.getSeconds()).padStart(2, '0')
      return `${dia}/${mes}/${año}, ${horas}:${minutos}:${segundos}`
    },
    async obtenerCotizacionDolar() {
      try {
        const timestamp = Date.now()
        const response = await axios.get('https://api.bluelytics.com.ar/v2/latest')
        if (response.data && response.data.oficial && response.data.oficial.value_sell) {
          const fechaFormateada = this.formatearFechaHora(timestamp)
          
          this.cotizacionDolar = response.data.oficial.value_sell
          this.timestampActualizacion = timestamp
          this.fechaActualizacion = fechaFormateada
        }
      } catch (error) {
        console.error('Error al obtener la cotización:', error)
      }
    },
    iniciarActualizacionAutomatica() {
      this.obtenerCotizacionDolar()
      this.intervaloActualizacion = setInterval(() => {
        this.obtenerCotizacionDolar()
      }, 2000)
    },
    detenerActualizacionAutomatica() {
      if (this.intervaloActualizacion) {
        clearInterval(this.intervaloActualizacion)
        this.intervaloActualizacion = null
      }
      this.fechaActualizacion = null
      this.timestampActualizacion = null
    }
  }
}
</script>

<style scoped>
.card {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>

