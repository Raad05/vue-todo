<script lang="ts" setup>
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue'
import type { Task } from './types'
import TaskList from './components/TaskList.vue'

const tasks = ref<Task[]>([])

const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  })
}

const toggleStatus = (id: string) => {
  const task = tasks.value.find((task) => task.id === id)
  if (task) {
    task.done = !task.done
  }
}
</script>

<template>
  <main>
    <h1>Task Tracker</h1>
    <TaskForm @add-task="addTask" />
    <h3>
      {{ !tasks.length ? 'Add a task to get started' : `0 / ${tasks.length} task(s) completed.` }}
    </h3>
    <TaskList :tasks @toggle-status="toggleStatus" />
  </main>
</template>

<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
}
</style>
