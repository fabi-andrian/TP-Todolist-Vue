<template>
  <fieldset role="group">
    <input 
    type="text"
    placeholder="Tâche à effectuer">
    <button>Ajouter</button>
  </fieldset>
  <div v-if="ToDo.length == 0">Vous n'avez pas de tâches à faire :(</div>
</template>

<script setup>
import { ref } from 'vue';

const ToDo = ref([])
</script>