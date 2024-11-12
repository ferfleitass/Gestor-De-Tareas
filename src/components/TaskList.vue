<template>
    <ul class="list-group">
      <li v-for="task in tasks" :key="task.id" class="list-group-item d-flex justify-content-between align-items-center">
        <span :class="{'text-decoration-line-through': task.completed}">{{ task.task }}</span>
        <button @click="toggleComplete(task)" class="btn btn-sm btn-success">Marcar como completada</button>
      </li>
    </ul>
  </template>
  
  <script>
  export default {
    name: 'TaskList',
    props: {
      tasks: Array
    },
    methods: {
      toggleComplete(task) {
        task.completed = !task.completed
      }
    }
  }
  </script>
  
  <style scoped>
  /* Estilos adicionales para una mejor presentación */
  .list-group-item {
    margin-bottom: 0.5rem;
    background-color: #f8f9fa;
    border-radius: 8px;
  }
  
  button {
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: #218838;
  }
  </style>
  