<script setup lang="ts">
import { ref } from 'vue'

// Interface TypeScript pour typer nos tâches
interface Task {
  id: number
  title: string
  completed: boolean
}

// État réactif : liste de tâches
const tasks = ref<Task[]>([
  { id: 1, title: 'Apprendre ref()', completed: true },
  { id: 2, title: 'Comprendre les directives', completed: false },
  { id: 3, title: 'Créer un composant', completed: false },
])

// v-model : lié à l'input pour la nouvelle tâche
const newTaskTitle = ref('')

// Compteur pour générer des IDs uniques
let nextId = 4

// Ajouter une tâche
function addTask() {
  if (newTaskTitle.value.trim()) {
    tasks.value.push({
      id: nextId++,
      title: newTaskTitle.value.trim(),
      completed: false,
    })
    newTaskTitle.value = ''  // Reset l'input
  }
}

// Toggle le statut d'une tâche
function toggleTask(task: Task) {
  task.completed = !task.completed
}

// Supprimer une tâche
function removeTask(id: number) {
  tasks.value = tasks.value.filter(t => t.id !== id)
}
</script>

<template>
  <div class="task-list">
    <h2>Liste de tâches</h2>

    <!-- v-model : liaison bidirectionnelle avec l'input -->
    <div class="add-task">
      <input
        v-model="newTaskTitle"
        placeholder="Nouvelle tâche..."
        @keyup.enter="addTask"
      />
      <!-- v-on : écouter l'événement click (@ est le raccourci de v-on:) -->
      <button @click="addTask">Ajouter</button>
    </div>

    <!-- v-if : affiche si la condition est vraie -->
    <p v-if="tasks.length === 0" class="empty">
      Liste vide - ajoutez une tâche !
    </p>

    <!-- v-else : s'affiche si le v-if précédent est faux -->
    <ul v-else>
      <!--
        v-for : itère sur le tableau
        :key est obligatoire pour aider Vue à tracker les éléments
      -->
      <li
        v-for="task in tasks"
        :key="task.id"
        @click="toggleTask(task)"
      >
        <!--
          v-bind : lie un attribut à une expression
          :class est le raccourci de v-bind:class
          Ici, la classe 'completed' est ajoutée si task.completed est true
        -->
        <span :class="{ completed: task.completed }">
          {{ task.title }}
        </span>

        <!-- .stop empêche la propagation (sinon toggleTask serait aussi appelé) -->
        <button @click.stop="removeTask(task.id)" class="delete">×</button>
      </li>
    </ul>

    <p class="count">{{ tasks.length }} tâche(s)</p>
  </div>
</template>

<style scoped>
.task-list {
  padding: 1.5rem;
  border: 2px solid #42b883;
  border-radius: 8px;
  max-width: 400px;
  margin: 2rem auto;
}

.add-task {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.add-task input {
  flex: 1;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-task button {
  padding: 0.5rem 1rem;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem;
  margin: 0.25rem 0;
  background: #f5f5f5;
  border-radius: 4px;
  cursor: pointer;
}

li:hover {
  background: #e8e8e8;
}

/* Classe conditionnelle appliquée via v-bind:class */
.completed {
  text-decoration: line-through;
  color: #888;
}

.delete {
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  cursor: pointer;
  font-size: 1rem;
  line-height: 1;
}

.empty {
  color: #888;
  font-style: italic;
}

.count {
  margin-top: 1rem;
  color: #666;
  font-size: 0.9rem;
}
</style>
