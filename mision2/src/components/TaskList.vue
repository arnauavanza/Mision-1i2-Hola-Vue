<template>
  <h2 class="form-title">Lista de tareas</h2>
  <div class="task-list">
    <div v-if="tasks.length === 0">No hay tareas disponibles.</div>
<!-- Looping through the tasks array and rendering a TaskItem component for each task, passing the task as a prop. -->
    <TaskItem v-for="task in tasks" :key="task.id" :task="task" />
  </div>

</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import TaskItem from './TaskItem.vue'
import type { Task } from '../interfaces/types';

// Task interface to define the structure of a task object.

const tasks = ref<Task[]>([]);

// Using the onMounted to load tasks from localStorage when the component is mounted.
onMounted(() => {
  const storedTasks = localStorage.getItem('tasks');
  if (storedTasks) {
    tasks.value = JSON.parse(storedTasks);
  }
});
</script>

<style scoped>
.form-title {
  margin-bottom: 10px;
  align-self: flex-start;
}
</style>