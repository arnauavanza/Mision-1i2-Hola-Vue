<template>
  <div class="container">
    <h1>Gestor de tareas</h1>
    <TaskForm @add="addTask" />
    <TaskList :tasks="tasks" @delete="deleteTask" @complete="completeTask"/>
  </div>
</template>

<script setup lang="ts">
// Main application component that serves as the entry point for the task management application.
import TaskForm from './components/TaskForm.vue'
import TaskList from './components/TaskList.vue'
import { ref, onMounted } from 'vue'
import type { Task } from './interfaces/types.ts'
const tasks = ref<Task[]>([])

onMounted(() => {
  const storedTasks = localStorage.getItem('tasks')

  if (storedTasks) {
    tasks.value = JSON.parse(storedTasks)
  }
})

function addTask(task: Task) {
  tasks.value.push(task)
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

function deleteTask(taskId: number) {
  const index = tasks.value.findIndex(task => task.id === taskId)

  if (index !== -1) {
    tasks.value.splice(index, 1)
  }

  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

function completeTask(taskId: number) {
  const task = tasks.value.find(task => task.id === taskId)

  if (task) {
    task.completed = true
  }

  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

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
