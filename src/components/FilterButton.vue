<script lang="ts" setup>
import type { TaskFilter } from '@/types'

const props = defineProps<{
  filter: TaskFilter
  currentFilter: TaskFilter
}>()

const emit = defineEmits<{
  setFilter: [filter: TaskFilter]
}>()
</script>

<template>
  <button
    :class="{ contrast: props.currentFilter === props.filter }"
    class="secondary"
    @click="emit('setFilter', props.filter)"
  >
    {{ props.filter }}
  </button>
</template>
