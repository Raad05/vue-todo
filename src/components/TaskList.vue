<script lang="ts" setup>
import type { Task } from '@/types'
import { TransitionGroup } from 'vue'

const props = defineProps<{ tasks: Task[] }>()

const emit = defineEmits<{
  toggleStatus: [id: string]
  removeTask: [id: string]
}>()
</script>

<template>
  <TransitionGroup name="list" tag="">
    <article v-for="task in props.tasks" :key="task.id" class="task">
      <label>
        <input type="checkbox" @input="emit('toggleStatus', task.id)" :checked="task.done" />
        <span :class="{ done: task.done }">{{ task.title }}</span>
      </label>
      <button class="outline" @click="emit('removeTask', task.id)">Remove</button>
    </article>
  </TransitionGroup>
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

/* transition-group */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
