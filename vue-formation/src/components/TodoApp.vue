<script setup lang="ts">
import { ref, computed } from 'vue'

interface Todo {
  id: number
  title: string
  completed: boolean
}

// État
const todos = ref<Todo[]>([
  { id: 1, title: 'Comprendre ref() et reactive()', completed: true },
  { id: 2, title: 'Maîtriser les directives Vue', completed: true },
  { id: 3, title: 'Créer une Todo List', completed: false },
])

const newTodoTitle = ref('')
const filter = ref<'all' | 'active' | 'completed'>('all')

let nextId = 4

// Computed : liste filtrée selon le filtre actif
const filteredTodos = computed(() => {
  switch (filter.value) {
    case 'active':
      return todos.value.filter(t => !t.completed)
    case 'completed':
      return todos.value.filter(t => t.completed)
    default:
      return todos.value
  }
})

// Computed : nombre de tâches restantes
const remainingCount = computed(() => {
  return todos.value.filter(t => !t.completed).length
})

// Computed : texte pluralisé
const remainingText = computed(() => {
  return remainingCount.value === 1 ? 'tâche restante' : 'tâches restantes'
})

// Actions
function addTodo() {
  const title = newTodoTitle.value.trim()
  if (title) {
    todos.value.push({
      id: nextId++,
      title,
      completed: false,
    })
    newTodoTitle.value = ''
  }
}

function toggleTodo(todo: Todo) {
  todo.completed = !todo.completed
}

function removeTodo(id: number) {
  todos.value = todos.value.filter(t => t.id !== id)
}

function clearCompleted() {
  todos.value = todos.value.filter(t => !t.completed)
}
</script>

<template>
  <div class="todo-app">
    <h2>Todo List</h2>

    <!-- Formulaire d'ajout -->
    <form @submit.prevent="addTodo" class="add-form">
      <input
        v-model.trim="newTodoTitle"
        placeholder="Qu'avez-vous à faire ?"
        autofocus
      />
      <button type="submit">Ajouter</button>
    </form>

    <!-- Liste des todos -->
    <ul v-if="filteredTodos.length" class="todo-list">
      <li v-for="todo in filteredTodos" :key="todo.id">
        <label :class="{ completed: todo.completed }">
          <input
            type="checkbox"
            :checked="todo.completed"
            @change="toggleTodo(todo)"
          />
          {{ todo.title }}
        </label>
        <button @click="removeTodo(todo.id)" class="delete">×</button>
      </li>
    </ul>

    <p v-else class="empty">
      {{ filter === 'all' ? 'Aucune tâche' : `Aucune tâche ${filter === 'active' ? 'active' : 'complétée'}` }}
    </p>

    <!-- Footer avec filtres -->
    <footer v-if="todos.length" class="footer">
      <span class="count">
        {{ remainingCount }} {{ remainingText }}
      </span>

      <!-- Filtres -->
      <div class="filters">
        <button
          :class="{ active: filter === 'all' }"
          @click="filter = 'all'"
        >
          Toutes
        </button>
        <button
          :class="{ active: filter === 'active' }"
          @click="filter = 'active'"
        >
          Actives
        </button>
        <button
          :class="{ active: filter === 'completed' }"
          @click="filter = 'completed'"
        >
          Complétées
        </button>
      </div>

      <!-- Clear completed -->
      <button
        v-if="todos.some(t => t.completed)"
        @click="clearCompleted"
        class="clear"
      >
        Effacer complétées
      </button>
    </footer>
  </div>
</template>

<style scoped>
.todo-app {
  max-width: 500px;
  margin: 2rem auto;
  padding: 1.5rem;
  border: 2px solid #42b883;
  border-radius: 12px;
  background: #fff;
}

h2 {
  margin: 0 0 1rem;
  color: #42b883;
}

.add-form {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.add-form input {
  flex: 1;
  padding: 0.75rem;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 1rem;
}

.add-form input:focus {
  outline: none;
  border-color: #42b883;
}

.add-form button {
  padding: 0.75rem 1.25rem;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
}

.add-form button:hover {
  background: #3aa876;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem;
  border-bottom: 1px solid #eee;
}

.todo-list li:last-child {
  border-bottom: none;
}

.todo-list label {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  cursor: pointer;
  flex: 1;
}

.todo-list input[type="checkbox"] {
  width: 20px;
  height: 20px;
  cursor: pointer;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

.delete {
  background: transparent;
  border: none;
  color: #e74c3c;
  font-size: 1.5rem;
  cursor: pointer;
  opacity: 0.5;
  padding: 0 0.5rem;
}

.delete:hover {
  opacity: 1;
}

.empty {
  color: #999;
  font-style: italic;
  text-align: center;
  padding: 2rem;
}

.footer {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 0.75rem;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #eee;
  font-size: 0.9rem;
}

.count {
  color: #666;
}

.filters {
  display: flex;
  gap: 0.25rem;
}

.filters button {
  padding: 0.25rem 0.75rem;
  background: transparent;
  border: 1px solid #ddd;
  border-radius: 4px;
  cursor: pointer;
  color: #666;
}

.filters button:hover {
  border-color: #42b883;
}

.filters button.active {
  border-color: #42b883;
  color: #42b883;
  font-weight: bold;
}

.clear {
  background: transparent;
  border: none;
  color: #e74c3c;
  cursor: pointer;
  text-decoration: underline;
}

.clear:hover {
  color: #c0392b;
}
</style>
