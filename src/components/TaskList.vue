<script lang="ts" setup>
import type { Task } from '@/types'

const props = defineProps<{ tasks: Task[] }>()

const emit = defineEmits<{
  toggleStatus: [id: string]
  removeTask: [id: string]
}>()
</script>

<template>
  <article v-for="task in props.tasks" :key="task.id" class="task">
    <label>
      <input type="checkbox" @input="emit('toggleStatus', task.id)" :checked="task.done" />
      <span :class="{ done: task.done }">{{ task.title }}</span>
    </label>
    <button class="outline" @click="emit('removeTask', task.id)">Remove</button>
  </article>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
