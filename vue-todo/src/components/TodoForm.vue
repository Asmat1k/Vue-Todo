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
        const formatDate = `${date.getDate()}.0 ${date.getMonth() + 1} at ${date.getHours()}:${date.getMinutes()}`;
        this.todo.time = formatDate;

        this.$emit('create', this.todo);

        this.todo.title = this.todo.body = '';
      }
    }
  };
</script>

<style>
  
</style>