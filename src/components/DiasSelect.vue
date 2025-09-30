<template>
  <form @submit.prevent="enviar">
    <label for="dia">Selecciona un día de la semana:</label>
    <select id="dia" v-model="diaSeleccionado" required>
      <option disabled value="">-- Selecciona un día --</option>
      <option v-for="dia in dias" :key="dia" :value="dia">{{ dia }}</option>
    </select>

    <button :disabled="!diaSeleccionado">Enviar</button>

    <p class="resultado" v-if="diaSeleccionado">
      Día seleccionado: <strong>{{ diaSeleccionado }}</strong>
    </p>
  </form>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'

const diaSeleccionado = ref('')
const dias = ['Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes', 'Sábado', 'Domingo']

watch(diaSeleccionado, (nuevo) => {
  localStorage.setItem('dia', nuevo)
})
onMounted(() => {
  diaSeleccionado.value = localStorage.getItem('dia') || ''
})

const enviar = () => {
  alert(`Día enviado: ${diaSeleccionado.value}`)
}
</script>

<style scoped>
label {
  display: block;
  margin-bottom: 0.5rem;
}
select {
  padding: 0.5rem;
  border-radius: 4px;
  border: 1px solid #a3bffa;
  background-color: #f6f8ff;
}
button {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background-color: #f1c1ea;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
.resultado {
  margin-top: 1rem;
  color: #333;
  transition: all 0.3s ease-in-out;
}
</style>
