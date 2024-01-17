<template>
  <div class="list" v-if="todos.length > 0">
    <TodoItem 
      v-for="todo in todos"
      :todo="todo"
      :key="todo.time"
      @remove="$emit('remove', todo)"
    />
  </div>
  <div v-else class="empty">List is empty...</div>
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

<style scoped>
  .list {
    display: flex;
    flex-direction: column;
    gap: 5px;

    padding: 0 5px 5px 5px;
  }
  .empty {
    display: flex;
    align-items: center;
    justify-content: center;

    text-align: center;
    text-transform: lowercase;
    color: #133471;

    height: 100%;
  }
</style>