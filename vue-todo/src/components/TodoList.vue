<template>
  <div>
    <h1>list</h1>
    <TodoItem 
      v-for="todo in todos"
      :todo="todo"
      :key="todo.time" 
    />
  </div>
</template>

<script>
  import TodoItem from './TodoItem.vue';

  export default {
    components: {
      TodoItem,
    },
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