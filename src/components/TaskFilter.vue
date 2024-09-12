<script setup>
defineProps({
  filter: String
});

// Define the 'emit' function to trigger events for parent components
//defineEmits is used to declare what custom events a component can emit
// In this case, it will be used to emit the 'update:filter' event.
const emit = defineEmits(['update:filter']);

// Function to update the filter value and notify the parent component about the change.
// This emits the 'update:filter' event with the new filter value passed as an argument.
const updateFilter = (newFilter) => {
  emit('update:filter', newFilter);
};

</script>

<template>
    <div class="btn-group mt-3" role="group" aria-label="Filter buttons">
      <input type="radio" class="btn-check" name="btnradio" id="btnradio1" autocomplete="off" :checked="filter === 'all'" @change="updateFilter('all')" />
      <label class="btn btn-outline-dark" for="btnradio1">All</label>
  
      <input type="radio" class="btn-check" name="btnradio" id="btnradio2" autocomplete="off" :checked="filter === 'pending'" @change="updateFilter('pending')" />
      <label class="btn btn-outline-secondary" for="btnradio2">Pending</label>
  
      <input type="radio" class="btn-check" name="btnradio" id="btnradio3" autocomplete="off" :checked="filter === 'completed'" @change="updateFilter('completed')" />
      <label class="btn btn-outline-success" for="btnradio3">Completed</label>
    </div>
  </template>
  

  