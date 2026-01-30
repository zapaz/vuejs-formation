<script setup lang="ts">
import UserCard from "./UserCard.vue";
import { ref } from "vue";
defineProps<{}>();

const users = ref([
  { name: "Alice", email: "alice@example.com" },
  { name: "Bob", email: "bob@example.com" },
  { name: "Charlie", email: "charlie@example.com" },
]);

const handleDelete = (email: string) => {
  const index = users.value.findIndex((user) => user.email === email);
  if (index !== -1) {
    users.value.splice(index, 1);
  }
};
</script>

<template>
  <UserCard v-for="user in users" :key="user.email" :name="user.name" :email="user.email" @delete="handleDelete" />
</template>

<style scoped></style>
