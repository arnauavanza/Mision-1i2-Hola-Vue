<template>
  <h2 class="form-title">Agregar una nueva tarea</h2>
  <form>
    <input v-model="taskInput" class="form-input" placeholder="Nueva tarea">
    <button @click="saveTask" type="submit">Añadir</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import type { Task } from '../interfaces/types';

const emit = defineEmits<{
  add: [task: Task]
}>()

// Reference to the input element and a reactive array to hold the tasks.
const taskInput = ref<string>('');

// Function to handle the form submission, creating a new task and emitting it to the parent component.
function saveTask(event: Event) {
  event.preventDefault()

  const text = taskInput.value.trim()

  if (!text) return

  const newTask: Task = {
    id: Date.now(),
    title: text,
    completed: false
  }

  emit('add', newTask)

  taskInput.value = ''
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.form-input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #0056b3;
}

.form-title {
  margin-bottom: 10px;
  align-self: flex-start;
}
</style>
