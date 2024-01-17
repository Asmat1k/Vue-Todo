<template>
  <div>
    <div>Title:{{ todo.title }}</div>
    <div>Text:{{ todo.body }}</div>
    <div>Time: {{ todo.time }}</div>
  </div>
</template>

<script>
  export default {
    props: {
      todo: {
        type: Object,
        required: true,
      }
    }
  }
</script>

<style>
  
</style>