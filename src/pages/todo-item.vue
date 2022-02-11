<template>
  <div class="todo-item">
    <div class="item-content">
      <a-checkbox v-model:checked="todo.completed" />
      <div class="item-title">{{ todo.title }}</div>
    </div>
    <a-button danger @click="delTodo">delete</a-button>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
const emits = defineEmits(['delTodo'])
interface Todo {
  id: number;
  title: string;
  completed: boolean
}
let props = defineProps<{ todo: Todo }>()
function delTodo() {
  emits('delTodo', props.todo.id)
}
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  font-size: 18px;
  border: 1px solid #ededed;
  border-top: none;
  padding: 0 12px;
}
.todo-item:first-child {
  border-top: 1px solid #ededed;
}
.item-content {
  display: flex;
}
.item-content :deep .ant-checkbox-wrapper {
  display: flex;
  align-items: center;
  width:48px;
}
.item-title {
  word-break: break-all;
  padding: 15px 15px 15px 0;
  display: inline-block;
  line-height: 1.2;
}
</style>
