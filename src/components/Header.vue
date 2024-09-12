<script setup>
defineProps({
  tasks: Array,
  completedTasks: Number
});
</script>

<template>
    <div>
      <h1 class="text-center p-4 mb-3">Todo Test Application</h1>
      <div class="form-label hstack gap-3 mb-4 h6 text-primary">
        <span>Total {{ tasks.length > 1 ? 'tasks' : 'task' }}: {{ tasks.length }}</span>
        <span class="ms-auto text-success">Completed Task: {{ completedTasks }}</span>
      </div>
    </div>
  </template>
  
