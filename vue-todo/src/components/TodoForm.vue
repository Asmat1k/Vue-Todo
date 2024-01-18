<template>
  <form class="form" @submit.prevent>
    <MyInput
      id="title"
      v-model="todo.title"
      maxlength="22"
      placeholder="Title..."
    />
    <MyInput
      id="body"
      v-model="todo.body"
      maxlength="70"
      placeholder="To do..."
    />
    <MyButton
      @click="handleClick"
    >
      Add
    </MyButton>
  </form>
  <div v-if="isError" class="error">Fill the form!</div>
</template>

<script>
  export default {
    props: {
      editedTodoId: {
        type: Number,
      },
    },
    data() {
      return {
        todo: {
          title: '',
          body: '',
        },
        isError: false,
      };
    },
    emits: ['func'],
    methods: {
      handleClick() {
        const date = new Date();
        const day = `${date.getDate()}`.padStart(2,0);
        const month =  `${date.getMonth() + 1}`.padStart(2,0);
        const hour = `${date.getHours()}`.padStart(2,0);
        const min = `${date.getMinutes()}`.padStart(2,0);
        const formatDate = `${day}.${month} at ${hour}:${min}`;

        this.todo.time = formatDate;
        if (this.editedTodoId <= -1){
          this.todo.id = Date.now()
        } else {
          this.todo.id = this.editedTodoId;
        }

        if (this.todo.title.length > 0 && this.todo.body.length > 0) {
          this.$emit('func', this.todo);

          this.setError(false);
          this.todo.title = this.todo.body = '';
        } else {
          this.setError(true);
        }
      },
      setError(boolean) {
        this.isError = boolean;
      },
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