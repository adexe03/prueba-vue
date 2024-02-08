<template>
  <p>
    <input type="text" placeholder="nueva tarea" @keyup.enter="$emit('insertTask', newTask)" v-model="newTask">
  </p>
</template>
<script setup>
import { ref } from 'vue';

const newTask = ref('');

// function insertTask() {
//   console.log('nueva tarea en componente: ' + newTask.value);

//   if (newTask.value.length > 2) {
//     $emit('insertNewTask');
//   }
// }
</script>
<style scoped>
p {
  background-color: aquamarine;
  padding: 10px;
}
</style>