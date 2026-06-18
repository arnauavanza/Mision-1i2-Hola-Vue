<template>
  <div class="container">
    <h1>Gestor de tareas</h1>
    <TaskForm />
    <TaskList />
  </div>
</template>

<script setup lang="ts">
// Main application component that serves as the entry point for the task management application.
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'
</script>

<style scoped>
.container {
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
