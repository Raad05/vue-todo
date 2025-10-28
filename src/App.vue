<script lang="ts" setup>
import { computed, ref } from 'vue'
import TaskForm from './components/TaskForm.vue'
import { type TaskFilter, type Task } from './types'
import TaskList from './components/TaskList.vue'
import FilterButton from './components/FilterButton.vue'

const tasks = ref<Task[]>([])
const filter = ref<TaskFilter>('All')

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

const totalDone = computed(() =>
  tasks.value.reduce((total, task) => (task.done ? total + 1 : total), 0),
)

const removeTask = (id: string) => {
  tasks.value = tasks.value.filter((task) => task.id !== id)
}

const setFilter = (newFilter: TaskFilter) => {
  filter.value = newFilter
}

const filteredTasks = computed(() => {
  switch (filter.value) {
    case 'All':
      return tasks.value
    case 'Todo':
      return tasks.value.filter((task) => !task.done)
    case 'Done':
      return tasks.value.filter((task) => task.done)
    default:
      return tasks.value
  }
})
</script>

<template>
  <main>
    <h1>Task Tracker</h1>
    <TaskForm @add-task="addTask" />
    <h3>
      {{
        !tasks.length
          ? 'Add a task to get started'
          : `${totalDone} / ${tasks.length} task(s) completed.`
      }}
    </h3>
    <div class="btn-container">
      <FilterButton :current-filter="filter" filter="All" @set-filter="setFilter" />
      <FilterButton :current-filter="filter" filter="Todo" @set-filter="setFilter" />
      <FilterButton :current-filter="filter" filter="Done" @set-filter="setFilter" />
    </div>
    <TaskList :tasks="filteredTasks" @toggle-status="toggleStatus" @remove-task="removeTask" />
  </main>
</template>

<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
}

.btn-container {
  display: flex;
  gap: 0.5rem;
  justify-content: end;
  margin-bottom: 1rem;
}
</style>
