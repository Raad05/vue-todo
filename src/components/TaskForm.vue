<script lang="ts" setup>
import { ref } from 'vue'

const newTask = ref('')

const emit = defineEmits<{
  addTask: [newTask: string]
}>()
const error = ref<string>('')

function formSubmitted() {
  if (newTask.value.trim()) {
    emit('addTask', newTask.value.trim())
    newTask.value = ''
  } else {
    error.value = 'Task cannot be empty'
  }
}
</script>

<template>
  <form @submit.prevent="formSubmitted">
    <label>
      New Task
      <input @input="error = ''" type="text" name="newTask" v-model="newTask" />
    </label>
    <small v-if="error">{{ error }}</small>
    <div class="btn-container">
      <button type="submit">Add</button>
    </div>
  </form>
</template>

<style scoped>
.btn-container {
  display: flex;
  justify-content: flex-end;
}

button {
  width: fit-content;
}
</style>
