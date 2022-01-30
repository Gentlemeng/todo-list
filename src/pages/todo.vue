<template>
  <h1 class="todo-h1">Todos</h1>
  <div class="todo-wrap">
    <!-- todo list input -->
    <div class="todo-header">
      <a-checkbox v-model:checked="checked">全选</a-checkbox>
      <a-input v-model:value="todoName" size="large" placeholder="What needs to be done?" />
    </div>

    <!-- todo list -->
    <todoList />
    <!-- todo list info -->
    <div></div>
  </div>
  
</template>

<script setup lang="ts">
import { defineComponent, ref } from 'vue'
import todoList from './todo-list.vue'
let checked = ref<boolean>(false)
let todoName = ref<string>('')
</script>

<style scoped>
.todo-h1 {
  margin: 0;
  font-size: 100px;
  font-weight: 100;
  text-align: center;
  color: rgba(175,47,47,0.15);
}
.todo-wrap {
  margin: 0 auto;
  width: 50%;
}
.todo-header {
  display: flex;
  align-items: center;
}
.todo-header .ant-input {
  flex: 1;
}
</style>
