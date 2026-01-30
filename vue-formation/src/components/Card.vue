<script setup lang="ts">


</script>

<template>
  <h1>UserCard</h1>

  <div class="card">
    <header>
      <slot name="header">Titre par défaut</slot>
    </header>

    <main>
      <slot>Contenu par défaut</slot>
    </main>

    <footer>
      <slot name="footer"></slot>
    </footer>
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
