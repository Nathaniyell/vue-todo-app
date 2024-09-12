<script setup>
import { ref, onMounted, computed, watch } from 'vue';
import Header from './components/Header.vue';
import TaskInput from './components/TaskInput.vue';
import TaskList from './components/TaskList.vue';
import TaskFilter from './components/TaskFilter.vue';

// `ref` creates a reactive reference that Vue tracks for changes.
// This is the tasks list which stores each task's details (task description and completion status).
const tasks = ref([]);  

// This is for the input field where users will enter a new task.
const newTask = ref(''); 

// `filter` tracks the current filter state (all, completed, or pending tasks).
const filter = ref('all'); 

// Error message to be displayed if input is invalid (e.g., empty task).
const errorMessage = ref(''); 

// `computed` property that calculates the number of completed tasks.
// It reacts to changes in the tasks list.
const completedTasks = computed(() => tasks.value.filter(task => task.completed).length);

// `onMounted` is a lifecycle hook that runs when the component is first rendered to the DOM.
// Here, we load the tasks from localStorage or fetch from an API if no local data is found.
onMounted(async () => {
  // Check if any tasks were stored in localStorage. If yes, parse and load them into `tasks`.
  const savedTasks = localStorage.getItem('tasks');
  tasks.value = savedTasks ? JSON.parse(savedTasks) : [];

  try {
    // Fetching sample tasks from a remote API.
    const response = await fetch('https://run.mocky.io/v3/16c30903-3570-44ea-a0e8-848cbeffc3a6');
    if (!response.ok) throw new Error('Network response was not ok');

    // Process and add fetched data to the tasks array.
    const data = await response.json();
    tasks.value = data.map(task => ({ task: task.task, completed: task.completed }));
  } catch (error) {
    // Log an error if the fetch fails.
    console.error('There was a problem with the fetch operation:', error);
  }
});

// Function to handle the submission of new tasks.
// It first checks if the input is valid, then adds the task to the tasks array.
const formSubmitHandler = () => {
  // Validate the input: check if it's not empty after trimming spaces.
  if (newTask.value.trim() === '') {
    // Show an error message and clear it after 5 seconds.
    errorMessage.value = "Input field is empty, please enter a task";
    setTimeout(() => { errorMessage.value = ''; }, 5000);
    return;
  }

  // If valid, push the new task to the `tasks` array.
  tasks.value.push({ task: newTask.value, completed: false });

  // Clear the input field after submitting.
  newTask.value = '';
};

// Function to remove a task from the tasks list based on its index.
const removeTask = (index) => {
  tasks.value.splice(index, 1); // `splice` removes the task at the specified index.
};

// `computed` property to filter tasks based on the current `filter` value.
// This computes a new array of tasks, filtered by completion status.
const filteredTasks = computed(() => {
  switch (filter.value) {
    case 'pending':
      return tasks.value.filter(task => !task.completed); // Show only pending tasks.
    case 'completed':
      return tasks.value.filter(task => task.completed); // Show only completed tasks.
    case 'all':
    default:
      return tasks.value; // Show all tasks by default.
  }
});

// `watch` function observes changes in the tasks array.
// When the tasks array is modified (e.g., task added/removed), it stores the updated array in localStorage.
watch(tasks, (newValue) => {
  localStorage.setItem('tasks', JSON.stringify(newValue)); // Update localStorage on every change to tasks.
}, { deep: true }); // `deep: true` ensures that changes within the array (e.g., task completion) are tracked.
</script>

<template>
  <main class="d-flex justify-content-center bg-light place-items-center align-items-center min-vh-100">
    
    <div class="col-md-8 col-lg-6 mx-auto px-4">
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
