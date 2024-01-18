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
      class="btn"
      @click="handleClick"
    >
      Add
    </MyButton>
    <div v-if="isError" class="error">It's empty...</div>
  </form>
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

        this.todo.done = false;
        this.todo.id = Date.now()

        if (this.todo.title.trim().length > 0 && this.todo.body.trim().length > 0) {
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

<style scoped>
  .form {
    position:  relative;

    display: flex;
    flex-direction: column;
    gap: 10px;

    border: 1px solid #173f88;
    border-radius: 10px;

    padding: 10px;
  }
  .btn {
    align-self: flex-end;
    padding: 5px 10px;
  }
  .error {
    position: absolute;
    bottom: 10px;
    right: 95px;


    text-transform: lowercase;
    text-align: center;
    color: red;

    padding: 5px;
  }
</style>