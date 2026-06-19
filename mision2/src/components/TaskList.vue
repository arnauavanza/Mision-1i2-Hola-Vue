<template>
  <h2 class="form-title">Lista de tareas</h2>
  <div class="task-list">
    <div v-if="props.tasks.length === 0">No hay tareas disponibles.</div>
<!-- Looping through the tasks array and rendering a TaskItem component for each task, passing the task as a prop. -->
    <TaskItem v-for="task in props.tasks" :key="task.id" :task="task" @delete="emit('delete', $event)" @complete="emit('complete', $event)"/>
  </div>

</template>

<script setup lang="ts">
import TaskItem from './TaskItem.vue'
import type { Task } from '../interfaces/types';

const props = defineProps<{
  tasks: Task[]
}>()

const emit = defineEmits<{
  delete: [id: number]
  complete: [id: number]
}>()

// // Function to delete a task by its ID, updating the tasks array and localStorage.
// function deleteTask(taskId: number) {
//   const index = tasks.value.findIndex(task => task.id === taskId);

//   if (index !== -1) {tasks.value.splice(index, 1);}
//   localStorage.setItem('tasks', JSON.stringify(tasks.value));
// }

// // Function to mark a task as completed by its ID, updating the tasks array and localStorage.
// function completeTask(taskId: number) {
//   const task = tasks.value.find(task => task.id === taskId);

//   if (task) {task.completed = true;}
//   localStorage.setItem('tasks',JSON.stringify(tasks.value));
// }
</script>

<style scoped>
.form-title {
  margin-bottom: 10px;
  align-self: flex-start;
}
</style>