<template>
  <TodoForm @create="createTodo"/>
  <TodoList :todos="todos" @remove="removeTodo"/>
</template>

<script>
  import TodoForm from './components/TodoForm.vue';
  import TodoList from './components/TodoList.vue';

  export default {
    components: { TodoForm, TodoList },
    data() {
      return {
        todos: [ { id: 0, title: 'Home', body: 'Do homework', time: '17.01 at 18:30'},  ],
      }
    },
    methods: {
      createTodo(todo) {
        const newTodo = {...todo};
        this.todos.push(newTodo);
      },
      removeTodo(todoToDelete) {
        this.todos = this.todos.filter((todo) => todo.id !== todoToDelete.id);
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
