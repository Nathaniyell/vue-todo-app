 
  <script setup>
  defineProps({
    filteredTasks: Array,
    removeTask: Function
  });
  </script>

<template>
    <ul v-if="filteredTasks.length !== 0" class="list-group mt-3">
      <li class="list-group-item hstack gap-3" v-for="(singleTask, index) in filteredTasks" :key="singleTask.id">
        <span :class="{ 'text-decoration-line-through': singleTask.completed }">
    {{ singleTask.title }}
  </span>
        <span class="hstack form-switch gap-3 ms-auto">
          <input type="checkbox" class="form-check-input" role="switch" v-model="singleTask.completed">
          <div class="vr"></div>
          <button class="btn btn-danger btn-sm" type="button" @click="removeTask(index)">Delete</button>
        </span>
      </li>
    </ul>
    <h4 class="text-danger text-center my-3" v-if="filteredTasks.length === 0">No tasks available</h4>
  </template>
 
  