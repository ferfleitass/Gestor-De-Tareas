<template>
  <div class="container-fluid">
    <div class="row">
      <!-- Barra de navegación -->
      <nav class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">Gestor de Tareas</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ms-auto">
              <li class="nav-item" @click="selectedView = 'add'">
                <a class="nav-link" href="#">Agregar Tarea</a>
              </li>
              <li class="nav-item" @click="selectedView = 'list'">
                <a class="nav-link" href="#">Lista de Tareas</a>
              </li>
              <li class="nav-item" @click="selectedView = 'combined'">
                <a class="nav-link" href="#">Vista Combinada</a>
              </li>
            </ul>
          </div>
        </div>
      </nav>

      <!-- Contenido -->
      <div class="col-12 mt-5 pt-5">
        <!-- Vista Agregar Tarea -->
        <div v-if="selectedView === 'add'" class="mt-5">
          <div class="card shadow-lg">
            <div class="card-header bg-primary text-white">
              <h3>Agregar Tarea</h3>
            </div>
            <div class="card-body">
              <TaskInput @add-task="addTask"/>
            </div>
          </div>
        </div>

        <!-- Vista Lista de Tareas -->
        <div v-if="selectedView === 'list'" class="mt-5">
          <div class="card shadow-lg">
            <div class="card-header bg-primary text-white">
              <h3>Lista de Tareas</h3>
            </div>
            <div class="card-body">
              <button class="btn btn-primary mb-3" @click="fetchTasksFromAPI">Cargar Tareas desde API</button>
              <TaskList :tasks="tasksFromAPI"/>
            </div>
          </div>
        </div>

        <!-- Vista Combinada -->
        <div v-if="selectedView === 'combined'" class="mt-5">
          <div class="card shadow-lg">
            <div class="card-header bg-primary text-white">
              <h3>Vista Combinada</h3>
            </div>
            <div class="card-body">
              <CombinedView :api-tasks="tasksFromAPI" @add-task="addTask"/>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import TaskInput from './components/TaskInput.vue'
import TaskList from './components/TaskList.vue'
import CombinedView from './components/CombinedView.vue'

export default {
  name: 'App',
  components: {
    TaskInput,
    TaskList,
    CombinedView
  },
  setup() {
    const tasksFromAPI = ref([])
    const selectedView = ref('add') // Vista inicial

    const addTask = (task) => {
      tasksFromAPI.value.push(task)
    }

    const fetchTasksFromAPI = async () => {
      const response = await fetch('https://dummyjson.com/todos')
      const data = await response.json()
      tasksFromAPI.value = data.todos
    }

    return { tasksFromAPI, selectedView, addTask, fetchTasksFromAPI }
  }
}
</script>

<style scoped>
.container-fluid {
  padding-top: 5rem; /* Para evitar que el contenido quede tapado por la navbar fija */
}

.navbar {
  background-color: #007bff; /* Azul de Bootstrap */
}

.card {
  margin-top: 2rem;
}

.card-header {
  font-size: 1.5rem;
}

.nav-link {
  cursor: pointer;
}

.nav-item:hover {
  text-decoration: underline;
}
</style>
