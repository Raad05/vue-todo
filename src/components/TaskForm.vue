<script lang="ts" setup>
import { ref } from 'vue'

const newTask = ref('')

const addTask = () => {
  console.log('====================================')
  console.log(newTask.value)
  console.log('====================================')
}
</script>

<template>
  <form @submit.prevent="addTask">
    <label>
      New Task
      <input type="text" name="newTask" v-model="newTask" />
    </label>
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
