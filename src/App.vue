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
      v-for="ToDo in sortedToDos()"
      :key="ToDo.date"
      :class="{completed: ToDo.completed}">
      <label>
        <input type="checkbox" v-model="ToDo.completed">
        {{ ToDo.title }}
      </label>
      </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideCompleted">
      Masquer les tâches complétées
    </label>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newToDo = ref ('')
const hideCompleted = ref(false)
const ToDos = ref([{
  title: 'Tâche 1',
  completed: true,
  date: 1,
},
{
  title: 'Tâche 2',
  completed: false,
  date: 2,
}])
const addTodo = () => {
  ToDos.value.push({
    title: newToDo.value,
    completed: false,
    date: Date.now(),
  })
  newToDo.value = ''
}
const sortedToDos = () => {
  const sortedToDos=  ToDos.value.toSorted((a,b) => a.completed > b.completed ? 1 : -1)
  if (hideCompleted.value == true){
    return sortedToDos.filter(t => t.completed == false)
  }
  return sortedToDos
}
</script>

<style>
.completed {
  opacity: .5;
  text-decoration: line-through;
}
</style>