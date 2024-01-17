<template>
  <TodoForm @create="createTodo"/>
  <TodoList :todos="todos" />
</template>

<script>
  import TodoForm from './components/TodoForm.vue';
  import TodoList from './components/TodoList.vue';

  export default {
    components: { TodoForm, TodoList },
    data() {
      return {
        todos: [ {title: 'Home', body: 'Do homework', time: '17.01 at 18:30'},  ],
      }
    },
    methods: {
      createTodo(todo) {
        const newTodo = {...todo};
        this.todos.push(newTodo);
      }
    }
};
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
</style>
