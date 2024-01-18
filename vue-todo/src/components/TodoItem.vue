<template>
  <div
    class="item"
  >
    <div class="content" v-bind:class="{ done: todo.done }" >
      <h5 class="title">{{ todo.title }}</h5>
      <div class="body">{{ todo.body }}</div>
      <time class="time">{{ todo.time }}</time>
    </div>
    <div class="btns">
      <MyButton
        @click="$emit('mark', todo)"
        v-bind:class="{ doneBtn: todo.done }"
      >
        ✔️
      </MyButton>
      <MyButton @click="$emit('remove', todo)">❌</MyButton>
    </div>    
  </div>
</template>

<script>
  import TodoForm from './TodoForm.vue';
  import MyButton from './UI/MyButton.vue';

  export default {
    props: {
      todo: {
        type: Object,
        required: true,
      }
    },
    components: { MyButton, TodoForm }
}
</script>

<style scoped>
  .item {
    display: flex;
    justify-content: space-between;
    gap: 15px;

    border: 1px solid #173f88;
    border-radius: 10px;

    padding: 10px;

    height: 40%;
  }
  .done {
    text-decoration: line-through;
  }
  .doneBtn {
    background-color:  #20d92070;
    border-color: #20d92070;
  }
  .content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 5px;

    word-wrap: break-word;

    height: 100%;
  }
  .title {
    justify-self: start;

    font-size: 15px;
    text-transform: capitalize;
  }
  .body {
    font-size: 13px;
    overflow-y: auto;

    min-height: 50px;
    height: 100%;
  }
  .body::-webkit-scrollbar-track {border-radius: 2px;}
  .body::-webkit-scrollbar {width: 4px;}
  .body::-webkit-scrollbar-thumb {border-radius: 2px;background: #6a7d9b;}
  .body:hover::-webkit-scrollbar-thumb {background: white;}
  .time {
    justify-self: end;
    font-size: 10px;
    font-weight: 600;
  }
  .btns {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    gap: 5px;
  }
</style>