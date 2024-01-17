<template>
  <form class="form" @submit.prevent>
    <MyInput
      id="title"
      v-model="todo.title"
      placeholder="Title..."
    />
    <MyInput
      id="body"
      v-model="todo.body"
      placeholder="To do..."
    />
    <MyButton
      @click="createToDo"
    >
      Add
    </MyButton>
  </form>
  <div v-if="isError" class="error">Fill the form!</div>
</template>

<script>
  export default {
    data() {
      return {
        todo: {
          title: '',
          body: '',
        },
        isError: false,
      };
    },
    emits: ['create'],
    methods: {
      createToDo() {
        const date = new Date();
        const formatDate = `${date.getDate()}.${date.getMonth() + 1} at ${date.getHours()}:${date.getMinutes()}`;
        
        this.todo.time = formatDate;
        this.todo.id = Date.now()

        if (this.todo.time > 0 || this.todo.body.length > 0) {
          this.$emit('create', this.todo);
          this.setError(false);
          this.todo.title = this.todo.body = '';
        } else {
          this.setError(true);
        }
      },
      setError(boolean) {
        this.isError = boolean;
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
  .error {
    text-align: center;
    color: red;
    font-weight: 700;
    margin: 10px 0;
  }
</style>