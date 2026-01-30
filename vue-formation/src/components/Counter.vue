<script setup lang="ts">
import { ref, computed } from 'vue'

// ref() crée une valeur réactive
// Pour les types primitifs (number, string, boolean), on utilise ref()
const count = ref(0)

// computed() crée une valeur dérivée qui se recalcule automatiquement
// quand ses dépendances changent
const double = computed(() => count.value * 2)

// Fonctions pour modifier le state
function increment() {
  count.value++  // Avec ref(), on accède à la valeur via .value
}

function decrement() {
  count.value--
}
</script>

<template>
  <div class="counter">
    <h2>Compteur: {{ count }}</h2>
    <p>Double: {{ double }}</p>

    <div class="buttons">
      <button @click="decrement">-1</button>
      <button @click="increment">+1</button>
    </div>
  </div>
</template>

<style scoped>
.counter {
  padding: 2rem;
  border: 2px solid #42b883;
  border-radius: 8px;
  text-align: center;
  max-width: 300px;
  margin: 2rem auto;
}

.buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-top: 1rem;
}

button {
  padding: 0.5rem 1.5rem;
  font-size: 1.2rem;
  cursor: pointer;
  border: none;
  border-radius: 4px;
  background: #42b883;
  color: white;
}

button:hover {
  background: #3aa876;
}
</style>
