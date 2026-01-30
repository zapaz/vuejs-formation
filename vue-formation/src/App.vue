<script setup lang="ts">
import Card from "./components/Card.vue";
import Counter from "./components/Counter.vue";
import UserList from "./components/UserList.vue";
</script>

<template>
  <div class="app">
    <h1>Formation Vue.js 3</h1>

    <div class="grid">
      <!-- Card avec Counter -->
      <Card>
        <template #header>
          <h2>Compteur</h2>
        </template>
        <Counter />
        <template #footer>
          <small>Module 1 : ref() et computed()</small>
        </template>
      </Card>

      <!-- Card avec UserList -->
      <Card>
        <template #header>
          <h2>Utilisateurs</h2>
        </template>
        <UserList />
        <template #footer>
          <small>Module 2 : props et emits</small>
        </template>
      </Card>
    </div>
  </div>
</template>

<style scoped>
.app {
  text-align: center;
  padding: 2rem;
  max-width: 900px;
  margin: 0 auto;
}

h1 {
  color: #42b883;
  margin-bottom: 2rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 1.5rem;
}
</style>
