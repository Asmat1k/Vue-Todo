<template>
  <div class="container">
    <div class="controls">
      <button 
        class="controls-btn"
        @click="changeViewMode"
        v-bind:class="{ active: !isViewModeOn }"
      >
        Add
      </button>
      <button
        class="controls-btn"
        v-bind:class="{ active: isViewModeOn }"
        @click="changeViewMode"
      >
        View
      </button>
    </div>
    <div class="content">
      <TodoForm
        v-if="!isViewModeOn"
        @func="createTodo"
      />
      <TodoList 
        v-else
        :todos="todos"
        @mark="markTodo"
        @remove="removeTodo"
        @change="changeViewMode"
      />
    </div>
    <div class="dev">dev by <a class="link" href="https://github.com/Asmat1k">asmat1k</a></div>
  </div>
</template>

<script>
  import TodoForm from './components/TodoForm.vue';
  import TodoList from './components/TodoList.vue';
  import MyButton from './components/UI/MyButton.vue';

  export default {
    components: { TodoForm, TodoList, MyButton },
    data() {
      return {
        todos: [],
        isViewModeOn: true,
      }
    },
    methods: {
      createTodo(todo) {
        const newTodo = {...todo};
        this.todos.push(newTodo);

        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      removeTodo(todoToDelete) {
        this.todos = this.todos.filter((todo) => todo.id !== todoToDelete.id);

        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      changeTodo(editedTodo) {
        this.todos = this.todos.map((todo) => {
          if (todo.id === editedTodo.id) {
            return {...todo, ...editedTodo};
          }
          return todo;
        })

        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      markTodo(markedTodo) {
        this.todos = this.todos.map((todo) => {
          if (todo.id === markedTodo.id) {
            return {...todo, done: !markedTodo.done};
          }
          return todo;
        })

        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      changeViewMode() {
        this.isViewModeOn = !this.isViewModeOn;
      }
    },
    mounted() {
      if (localStorage.getItem('todos')) {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      }
    }
};
</script>

<style> 
  @import url('https://fonts.googleapis.com/css2?family=Afacad:wght@400;500;600;700&family=Roboto:wght@400;500;700;900&display=swap');
  * {
    font-family: 'Roboto', sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  } 
  #app {
    z-index: 2;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #3c7aed;

    padding: 0 15px;
    height: 100vh;
  }
  .container {
    display: flex;
    flex-direction: column;
    gap: 10px;

    background-color: cornflowerblue;
    border-radius: 10px;

    width: 320px;
    height: 420px;

    padding: 10px;
  }
  .controls {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
  }
  .content {
    overflow-y: auto;
    height: 100%;
  }
  .content::-webkit-scrollbar-track {border-radius: 2px;}
  .content::-webkit-scrollbar {width: 4px;}
  .content::-webkit-scrollbar-thumb {border-radius: 2px;background: #6a7d9b;}
  .content:hover::-webkit-scrollbar-thumb {background: white;}
  .controls-btn {
    cursor: pointer;
    
    background-color: transparent;
    border: 1px solid #173f88;
    border-radius: 10px;

    text-transform: uppercase;
    font-weight: 700;
    color: #173f88;
    padding: 10px 15px;

    width: 100%;
  }
  .active {
    background-color: transparent;
    border: 1px solid #173f88;
    border-radius: 10px;

    text-transform: uppercase;
    font-weight: 700;
    background-color: #173f88;
    color: white;
    padding: 10px 15px;

    width: 100%;
  }
  .dev {
    text-align: center;
    color: #02266a;
    font-size: 10px;
  }
  .link {
    color: #02266a; 
  }
</style>
