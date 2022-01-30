<template>
  <div class="todo-list">
    <todoItem
      v-for="item in todoItems"
      :key="item.id"
      :value='item.name'
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import todoItem from './todo-item.vue'
let todoItems = ref([
  { id: '1', name: '121'}
])
</script>

<style scoped>

</style>
