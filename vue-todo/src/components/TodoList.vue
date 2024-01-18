<template>
  <div class="list" v-if="todos.length > 0">
    <TodoItem 
      v-for="todo in todos"
      :todo="todo"
      :key="todo.id"
      @mark="$emit('mark', todo)"
      @remove="$emit('remove', todo)"
      @change="$emit('change', todo)"
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
    display: inline-flex;
    justify-content: start;
    flex-direction: column;
    gap: 5px;

    padding: 0 5px 5px 5px;

    width: 100%;
    height: 100%;
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