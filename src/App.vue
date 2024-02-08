<template lang="">
  <h1>Lista de tareas</h1>
  <CreateTask @insert-task="insertTask"/>
  <p>
    <input type="text" placeholder="nueva tarea" @keyup.enter="insertTask" v-model="newTask">
  </p>
  <p>Nueva ID: {{ newID }}</p>
  <p>Se han encontrado {{tasks.length}} tarea/s</p>
  <p>{{ textoNumeroTareas }}</p>
  <ul>
    <li v-for='task of tasks' :key='task.id' @click="removeTask(task.id)">
      {{task.id}} - {{task.name}}
    </li>
  </ul>
</template>
<script setup>
import { computed, ref } from 'vue';
import CreateTask from './components/CreateTask.vue';

const tasks = ref([
  { id: 1, name: 'Corregir exámenes del lado del servidor' },
  { id: 2, name: 'Corregir exámenes del lado del cliente' },
  { id: 3, name: 'Corregir exámenes de recuperación' },
  { id: 4, name: 'Preparar examen chungo de Vue' },
]);

const newTask = ref('');

const textoNumeroTareas = computed(() => {
  if (tasks.value.length == 0) return "No hay tareas";
  else if (tasks.value.length == 1) return "Hay una tarea";
  return "Hay " + tasks.value.length + " tareas";
});

function insertTask(txt) {
  console.log('Insertando nueva tarea...');
  console.log(txt);
  tasks.value.push({
    id: newID.value,
    name: txt
  });
}

const newID = computed(() => {
  const max = Math.max(...tasks.value.map(t => t.id)) + 1;
  return max < 0 ? 1 : max;
});

function removeTask(id) {
  tasks.value = tasks.value.filter(t => t.id !== id);
}
</script>
<style lang="">
  
</style>