<template>
  <h2 class="form-title">Agregar una nueva tarea</h2>
  <form>
    <input v-model="taskInput" class="form-input" placeholder="Nueva tarea">
    <button @click="saveTask" type="submit">Añadir</button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// Task interface to define the structure of a task object.
interface Task {
  id: number;
  title: string;
  completed: boolean;
}

// Reference to the input element and a reactive array to hold the tasks.
const taskInput = ref<string>('');
const tasks = ref<Task[]>(JSON.parse(localStorage.getItem('tasks') || '[]'));

// Function to save a new task to the tasks array and localStorage.
function saveTask() {
  if (taskInput.value) {
    const newTask: Task = {
      id: Date.now(),
      title: taskInput.value.trim(),
      completed: false,
    };
    if (newTask.title) {
      tasks.value.push(newTask);
      taskInput.value = '';
      localStorage.setItem('tasks', JSON.stringify(tasks.value));

    } else {
      alert('Por favor, ingresa un título para la tarea.');
    }
  }
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
