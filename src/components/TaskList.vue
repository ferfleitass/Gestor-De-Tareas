<template>
  <ul class="list-group">
    <li v-for="task in tasks" :key="task.id" class="list-group-item d-flex justify-content-between align-items-center">
      <!-- Cambiado 'task.task' por 'task.todo' -->
      <span :class="{'text-decoration-line-through': task.completed}">{{ task.todo }}</span>
      <button @click="toggleComplete(task)" class="btn btn-sm btn-success">
        Marcar como completada
      </button>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  methods: {
    toggleComplete(task) {
      task.completed = !task.completed; // Alterna el estado de completado
    },
  },
};
</script>

<style scoped>
.text-decoration-line-through {
  text-decoration: line-through;
}
</style>
