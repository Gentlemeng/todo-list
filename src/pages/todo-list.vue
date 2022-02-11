<template>
  <div class="todo-list">
    <todoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      v-bind="$attrs"
    />
  </div>
</template>

<script setup lang="ts">
// https://dexie.org/
import todoItem from './todo-item.vue'
defineProps({
  todos: Array,
})
</script>

<style scoped>
.todo-list {
  margin-top: 12px;
}
</style>
