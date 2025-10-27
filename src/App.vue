<script lang="ts" setup>
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue'
import type { Task } from './types'

const tasks = ref<Task[]>([])

const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  })
}
</script>

<template>
  <main>
    <h1>Task Tracker</h1>
    <TaskForm @add-task="addTask" />
    <article v-for="task in tasks" :key="task.id">
      {{ task.title }}
    </article>
  </main>
</template>

<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
}
</style>
