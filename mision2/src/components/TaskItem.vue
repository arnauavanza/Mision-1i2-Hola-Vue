<template>
  <div class="task-item">
<!-- Conditional to render the task title with a strikethrough if it is completed, otherwise render it normally. -->
    <div v-if="!props.task.completed">{{ props.task.title }}</div>
    <div v-else class="completed-task">{{ props.task.title }}</div>
    <form>
<!-- Button calling the deleteTask function. -->
      <button class="delete-button" type="submit" @click="deleteTask(props.task.id)">Eliminar</button>
    </form>
    <form>
<!-- Button calling the completeTask function. -->
      <button class="complete-button" type="submit" @click="completeTask(props.task.id)">Completar</button>
    </form>

  </div>
</template>

<script setup lang="ts">

// Task interface to define the structure of a task object.
interface Task {
  id: number;
  title: string;
  completed: boolean;
}

// ComponentProps interface to define the props expected by the component.
interface ComponentProps {
  task: Task
}

const props = defineProps<ComponentProps>();

// Function to delete a task from localStorage based on its ID.
function deleteTask(taskId: number) {
  const tasks: Task[] = JSON.parse(localStorage.getItem('tasks') || '[]');
  const index = tasks.findIndex(task => task.id === taskId);
  if (index !== -1) {
    tasks.splice(index, 1); 
    localStorage.setItem('tasks', JSON.stringify(tasks));
  }
}

// Function to mark a task as completed in localStorage based on its ID.
function completeTask(taskId: number) {
  const tasks: Task[] = JSON.parse(localStorage.getItem('tasks') || '[]');
  for (const task of tasks) {
    if (task.id === taskId) {
      task.completed = true;
      break;
    }
  }
  localStorage.setItem('tasks', JSON.stringify(tasks));
}

</script>

<style scoped>
.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-bottom: 10px;
}

.delete-button {
  padding: 5px 10px;
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.delete-button:hover {
  background-color: #c82333;
}

.complete-button {
  background-color: #28a745;
  padding: 5px 10px;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.complete-button:hover {
  background-color: #218838;
}

.completed-task {
  text-decoration: line-through;
  color: #6c757d;
}
</style>
