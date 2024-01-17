<template>
  <div v-for="todo in todos">
    <div>Title:{{ todo.title }}</div>
    <div>Text:{{ todo.body }}</div>
    <div>Time: {{ todo.time }}</div>
  </div>
</template>

<script>
  export default {
    props: {
      todos: {
        type: Array,
        required: true,
      }
    },
  };
</script>

<style>
  
</style>