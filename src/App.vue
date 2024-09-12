<script setup>
import { ref, onMounted, computed, watch } from 'vue';
import Header from './components/Header.vue';
import TaskInput from './components/TaskInput.vue';
import TaskList from './components/TaskList.vue';
import TaskFilter from './components/TaskFilter.vue';


const tasks = ref([]);
const newTask = ref('');
const filter = ref('all');
const errorMessage = ref('');
const completedTasks = computed(() => tasks.value.filter(task => task.completed).length);

const fetchTasks = async()=>{
  try {
    // Fetching sample tasks from a remote API.
 const response = await fetch('https://run.mocky.io/v3/16c30903-3570-44ea-a0e8-848cbeffc3a6');
    
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`); // Handle HTTP error
    }
    const data = await response.json();
    tasks.value = data.map(task => ({ task: task.task, completed: task.completed }));
  } catch (error) {

    console.error('There was a problem with the fetch operation:', error);
  }
}

onMounted(() => {
  fetchTasks()
  const savedTasks = localStorage.getItem('tasks');
  tasks.value = savedTasks ? JSON.parse(savedTasks) : [];
});

const formSubmitHandler = () => {

  if (newTask.value.trim() === '') {

    errorMessage.value = "Input field is empty, please enter a task";
    setTimeout(() => { errorMessage.value = ''; }, 5000);
    return;
  }
  tasks.value.push({ task: newTask.value, completed: false });
  newTask.value = '';
};


const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

const filteredTasks = computed(() => {
  switch (filter.value) {
    case 'pending':
      return tasks.value.filter(task => !task.completed);
    case 'completed':
      return tasks.value.filter(task => task.completed);
    case 'all':
    default:
      return tasks.value;
  }
});

watch(tasks, (newValue) => {
  localStorage.setItem('tasks', JSON.stringify(newValue));
}, { deep: true }); 
</script>


<template>
  <main class="d-flex justify-content-center bg-light place-items-center align-items-center min-vh-100">    <div class="col-md-8 col-lg-6 mx-auto px-4">
      <Header :tasks="tasks" :completedTasks="completedTasks" />

      <!--    The `v-model:newTask` binds the input value to the `newTask` ref, and `formSubmitHandler` handles submission. -->
      <TaskInput v-model:newTask="newTask" :errorMessage="errorMessage" :formSubmitHandler="formSubmitHandler" />  
      
      <!-- Render the filtered tasks list and allows task deletion. -->
      <TaskList :filteredTasks="filteredTasks" :removeTask="removeTask" />  
      
      <!-- The `v-model:filter` binds the filter state to the `filter` ref. -->
      <TaskFilter v-model:filter="filter" />
    </div>
  </main>
</template>
