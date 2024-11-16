<template>
  <div class="fetch-tasks p-3">
    <h3>Extraer Tareas</h3>
    <button class="btn btn-success" @click="fetchTasks">Obtener Tareas</button>
    <ul class="list-group mt-3">
      <li class="list-group-item" v-for="task in tasks" :key="task.id">
        {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await fetch('https://dummyjson.com/todos');
        const data = await response.json();
        this.tasks = data.todos.slice(0, 10); // Limitar a 10 tareas
      } catch (error) {
        console.error('Error al obtener tareas:', error);
      }
    },
  },
};
</script>
