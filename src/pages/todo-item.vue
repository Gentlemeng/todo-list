<template>
  <div class="todo-item">{{ value }}</div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
let props = defineProps({
  value: String,
})
</script>

<style scoped>

</style>
