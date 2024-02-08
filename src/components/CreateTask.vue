<template>
  <p>
    <input type="text" placeholder="nueva tarea" @keyup.enter="insertTask" v-model="newTask">
  </p>
</template>
<script setup>
import { ref } from 'vue';
const emit = defineEmits(['insertTask']);

const newTask = ref('');

function insertTask() {
  console.log('nueva tarea en componente: ' + newTask.value);
  if (newTask.value.length > 2) {
    emit('insertTask', newTask.value);
    newTask.value = '';
  }
}
</script>
<style scoped>
p {
  background-color: aquamarine;
  padding: 10px;
}
</style>