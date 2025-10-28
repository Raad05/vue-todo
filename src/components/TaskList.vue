<script lang="ts" setup>
import type { Task } from '@/types'

const props = defineProps<{ tasks: Task[] }>()

const emit = defineEmits<{
  toggleStatus: [id: string]
}>()
</script>

<template>
  <article v-for="task in props.tasks" :key="task.id">
    <label>
      <input type="checkbox" @input="emit('toggleStatus', task.id)" :checked="task.done" />
      <span :class="{ done: task.done }">{{ task.title }}</span>
    </label>
  </article>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
