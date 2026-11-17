<script setup>
import { ref } from 'vue';
import PhaserCanvas from './components/PhaserCanvas.vue';

const nom = ref('Anna');
const mostrarJoc = ref(true);

const colorAvatar = ref('#10b981');
const estado = ref('Disponible');
const pausat = ref(false);

const phaserCanvas = ref(null);

function canviarPausa() {
  pausat.value = !pausat.value;
  phaserCanvas.value?.canviarPausa(pausat.value);
}
</script>

<template>
  <main class="contenidor-app">
    <div class="controls">

      <input v-model="nom" placeholder="Escriu el teu nom d'usuari..." />

      <!-- Selector de color -->
      <label>Color de l'avatar:</label>
      <input type="color" v-model="colorAvatar" />

      <!-- Selector de estado -->
      <label>Estat:</label>
      <select v-model="estado">
        <option>Disponible</option>
        <option>Ocupat</option>
        <option>Absent</option>
      </select>

      <!-- Botón de pausa -->
      <button @click="canviarPausa">
        {{ pausat ? 'Reprèn' : 'Pausa' }}
      </button>

      <button @click="mostrarJoc = !mostrarJoc">
        {{ mostrarJoc ? 'Amaga el llenç' : 'Mostra el llenç' }}
      </button>

    </div>

    <PhaserCanvas
      v-if="mostrarJoc"
      ref="phaserCanvas"
      :nomUsuari="nom"
      :colorAvatar="colorAvatar"
      :estat="estado"
    />
  </main>
</template>