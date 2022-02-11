<template>
  <h1 class="todo-h1">Todos</h1>
  <div class="todo-wrap">
    <!-- todo list input -->
    <div class="todo-header">
      <a-checkbox v-model:checked="allChecked">全选</a-checkbox>
      <a-input
        v-model:value="todoTitle"
        size="large"
        placeholder="What needs to be done?"
        @keydown.enter="addTodo"
      />
    </div>

    <!-- todo list -->
    <todoList :todos="todosFilter" @delTodo="delTodo" />
    <div class="todo-footer">
      <div class="todos-left">
        {{active.length}} item left
      </div>
      <div class="todos-tabs">
        <a-radio-group v-model:value="todosType" size="large">
          <a-radio-button :value="0">All</a-radio-button>
          <a-radio-button :value="1">Active</a-radio-button>
          <a-radio-button :value="2">Completed</a-radio-button>
        </a-radio-group>
      </div>
      <div class="todos-clear">
        <a-button danger :disabled="!completed.length" @click="clearCompleted">Clear completed</a-button>
      </div>
    </div>
  </div>
  
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import todoList from './todo-list.vue'
interface Todo {
  id: number;
  title: string;
  completed: boolean
}
let todos = ref<Array<Todo>>([])
let checked = ref<boolean>(false)
let todoTitle = ref<string>('')
let todosType = ref<number>(0)

let todosFilter = computed(() => {
  if(todosType.value === 0) {
    return todos.value
  }
  // active
  if (todosType.value === 1) {
    return active.value
  }
  // completed
  if (todosType.value === 2) {
    return todos.value.filter(todo => todo.completed)
  }
  return []
})

let active = computed(() => {
  return todos.value.filter(todo => !todo.completed)
})
let completed = computed(() => {
  return todos.value.filter(todo => todo.completed)
})

let allChecked = computed({
  get() {
    if (!todos.value.length) {
      return false
    }
    return !active.value.length
  },
  set(value:boolean) {
    todos.value.forEach(todo => todo.completed = value)
  }
})

function addTodo () {
  if (!todoTitle.value.trim()) return
  const lastTodo:Todo = todos.value[todos.value.length - 1]
  let id:number = lastTodo ? lastTodo.id : 0
  todos.value.push({ id: ++id, title: todoTitle.value, completed: false})
  todoTitle.value = ''
}
function delTodo(id: number) {
  const index = todos.value.findIndex(todo => todo.id === id)
  todos.value.splice(index, 1)
}
function clearCompleted() {
  todos.value = todos.value.filter(todo => !todo.completed)
}
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
  color: #4d4d4d;
}
.todo-header {
  display: flex;
  align-items: center;
}
.todo-header .ant-input {
  flex: 1;
}
.todo-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 12px;
}
</style>
