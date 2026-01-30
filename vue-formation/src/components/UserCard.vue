<script setup lang="ts">

defineProps<{ name: string; email: string}>();

const emit = defineEmits<{
  (e: 'delete', email: string): void
}>()

 
</script>

<template>
  <h1>UserCard</h1>

  <div class="card">
    <p>User Name: {{ name }}</p>
    <p>User Email: {{ email }}</p>
    <button @click="emit('delete', email)">Supprimer</button>
  </div>
</template>

<style scoped>
.card {
  border: 1px solid #ccc;
  padding: 1rem;
  margin: 1rem;
  border-radius: 0.5rem;
}
</style>
