<template>
  <form class="form" @submit.prevent>
    <MyInput
      v-model="todo.title"
      placeholder="Title..."
    />
    <MyInput
      v-model="todo.body"
      placeholder="Body..."
    />
    <MyButton
      @click="createToDo"
    >
    Add
    </MyButton>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        todo: {
          title: '',
          body: '',
        }
      };
    },
    methods: {
      createToDo() {
        const date = new Date();
        const formatDate = `${date.getDate()}.${date.getMonth() + 1} at ${date.getHours()}:${date.getMinutes()}`;
        
        this.todo.time = formatDate;
        this.todo.id = Date.now()

        this.$emit('create', this.todo);

        this.todo.title = this.todo.body = '';
      }
    }
  };
</script>

<style>
  .form {
    display: flex;
    flex-direction: column;
    gap: 10px;

    border: 1px solid #173f88;
    border-radius: 10px;

    padding: 10px;
  }
</style>