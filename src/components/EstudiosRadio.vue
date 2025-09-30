<template>
  <fieldset role="radiogroup" aria-labelledby="estudios-label">
    <legend id="estudios-label">¿Qué tipo de estudios tienes?</legend>

    <label v-for="opcion in opciones" :key="opcion" :for="opcion">
      <input
        type="radio"
        :id="opcion"
        :value="opcion"
        v-model="estudios"
        name="estudios"
      />
      {{ opcion }}
    </label>

    <p class="resultado">Seleccionado: <strong>{{ estudios }}</strong></p>
  </fieldset>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'

const estudios = ref('')
const opciones = ['Primarios', 'Secundarios', 'Universitarios', 'Postgrado']

watch(estudios, (nuevo) => {
  localStorage.setItem('estudios', nuevo)
})
onMounted(() => {
  estudios.value = localStorage.getItem('estudios') || ''
})
</script>

<style scoped>
fieldset {
  margin-bottom: 2rem;
  border: 2px dashed #a3bffa;
  padding: 1rem;
  border-radius: 8px;
  background-color: #f6f8ff;
}
label {
  display: block;
  margin: 0.5rem 0;
  cursor: pointer;
}
.resultado {
  margin-top: 1rem;
  color: #333;
  transition: all 0.3s ease-in-out;
}
</style>
