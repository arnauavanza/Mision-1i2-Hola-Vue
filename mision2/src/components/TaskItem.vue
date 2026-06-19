<template>
  <div class="task-item">
<!-- Conditional to render the task title with a strikethrough if it is completed, otherwise render it normally. -->
    <div :class="{ 'completed-task': props.task.completed }">{{ props.task.title }}</div>
<form @submit.prevent="handleSubmit">
  <button type="submit" class="delete-button" value="delete" name="action">Eliminar</button>
  <button type="submit" class="complete-button" value="complete" name="action">Completar</button>
</form> 
  </div>
</template>

<script setup lang="ts">
import type { Task } from '../interfaces/types';

// ComponentProps interface to define the props expected by the component.
interface ComponentProps {
  task: Task
}

const props = defineProps<ComponentProps>();
  
const emit = defineEmits<{
  delete: [id: number]
  complete: [id: number]
}>();

const handleSubmit = (event: SubmitEvent) => {
  const submitter = event.submitter as HTMLButtonElement

  switch (submitter.value) {
    case 'delete':
      emit('delete', props.task.id)
      break

    case 'complete':
      emit('complete', props.task.id)
      break
  }
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
  margin-right: 5px;
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
