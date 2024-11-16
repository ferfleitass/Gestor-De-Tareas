<template>
    <div>
      <TaskList :tasks="apiTasks" />
      <TaskInput @add-task="addTask" />
    </div>
  </template>
  
  <script>
  import TaskInput from './TaskInput.vue'
  import TaskList from './TaskList.vue'
  
  export default {
    name: 'CombinedView',
    props: {
      apiTasks: Array
    },
    components: {
      TaskInput,
      TaskList
    },
    methods: {
      addTask(task) {
        this.$emit('add-task', task)
      }
    }
  }
  </script>
  
