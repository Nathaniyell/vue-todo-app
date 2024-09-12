<script setup>
  defineProps({
    newTask: String,
    errorMessage: String,
    formSubmitHandler: Function
  });
  
  const emit = defineEmits(['update:newTask']);
  const updateTask = (value) => {
    emit('update:newTask', value);
  };
  </script>
  

<template>
    <form @submit.prevent="formSubmitHandler" class="input-group">
      <input type="text" id="newTask" class="form-control" name="newTask" :value="newTask" @input="updateTask($event.target.value)" />
      <button class="btn btn-primary btn-sm" type="submit">Add Task</button>
    </form>
    <p class="text-danger">{{ errorMessage }}</p>
  </template>
  
  