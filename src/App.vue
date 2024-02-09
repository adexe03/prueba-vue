<template lang="">
  <p>
    Opción:
    <select v-model="option">
      <option value="list">Listado</option>
      <option value="create">Crear tarea</option>
    </select>
  </p>
  <div v-if="option=='list'">
    <h1>Lista de tareas</h1>
    <p>
      Filtro:
      <input type="text" placeholder="Filtrar..." v-model="wordSearch">
    </p>
    <p>Se han encontrado {{tasks.length}} tarea/s</p>
    <p>{{ textoNumeroTareas }}</p>
    <ul>
      <ViewTask v-for="task of filteredTasks" :key="task.id" :task="task" @remove-task="removeTask"/>
    </ul>
    <ul>
      <li v-for='task of tasks' :key='task.id' @click="removeTask(task.id)">
        {{task.id}} - {{task.name}}
      </li>
    </ul>
  </div>
  <CreateTask v-else @insert-task="insertTask"/>
</template>

<script setup>
import { computed, ref } from 'vue';
import CreateTask from './components/CreateTask.vue';
import ViewTask from './components/ViewTask.vue';

const option = ref('list');

const tasks = ref([
  { id: 1, name: 'Corregir exámenes del lado del servidor' },
  { id: 2, name: 'Corregir exámenes del lado del cliente' },
  { id: 3, name: 'Corregir exámenes de recuperación' },
  { id: 4, name: 'Preparar examen chungo de Vue' },
]);

const wordSearch = ref('');

const newTask = ref('');

const textoNumeroTareas = computed(() => {
  if (tasks.value.length == 0) return "No hay tareas";
  else if (tasks.value.length == 1) return "Hay una tarea";
  return "Hay " + tasks.value.length + " tareas";
});

function insertTask(task) {
  console.log('Insertando nueva tarea...');
  console.log(task);
  tasks.value.push({
    id: newID.value,
    name: task
  });
}

const newID = computed(() => {
  const max = Math.max(...tasks.value.map(t => t.id)) + 1;
  return max < 0 ? 1 : max;
});

function removeTask(id) {
  tasks.value = tasks.value.filter(t => t.id !== id);
}

const filteredTasks = computed(() => {
  return tasks.value.filter(t => t.name.toLocaleLowerCase().includes(wordSearch.value.toLocaleLowerCase()));
});
</script>

<style lang="">
  
</style>