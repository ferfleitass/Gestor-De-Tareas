<template>
    <div class="mb-3">
      <input
        v-model="taskName"
        type="text"
        class="form-control"
        placeholder="Ingrese una nueva tarea"
      />
      <button @click="submitTask" class="btn btn-success mt-3 w-100">Agregar Tarea</button>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  export default {
    name: 'TaskInput',
    setup(props, { emit }) {
      const taskName = ref('')
  
      const submitTask = () => {
        if (taskName.value) {
          emit('add-task', { id: Date.now(), task: taskName.value, completed: false })
          taskName.value = ''
        }
      }
  
      return { taskName, submitTask }
    }
  }
  </script>
  
  <style scoped>
  /* Estilos para mejorar la apariencia */
  button {
    transition: all 0.3s ease;
  }
  
  button:hover {
    background-color: #28a745;
  }
  </style>
  