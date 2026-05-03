<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
    <input 
    v-model="newToDo"
    type="text"
    placeholder="Tâche à effectuer">
    <button :disabled="newToDo.length == 0">Ajouter</button>
  </fieldset>
  </form>
  <div v-if="ToDos.length == 0">Vous n'avez pas de tâches à faire :(</div>
  <div v-else>
    <ul>
      <li 
      v-for="ToDo in ToDos"
      :key="ToDo.date">
    {{ ToDo.title }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newToDo = ref ('')
const ToDos = ref([])
const addTodo = () => {
  ToDos.value.push({
    title: newToDo.value,
    completed: false,
    date: Date.now(),
  })
  newToDo.value = ''
}
</script>