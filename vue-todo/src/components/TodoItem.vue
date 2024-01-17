<template>
  <div class="item">
    <div class="content">
      <h5 class="title">{{ todo.title }}</h5>
      <div class="body">- {{ todo.body }}</div>
      <time class="time">{{ todo.time }}</time>
    </div>
    <MyButton @click="$emit('remove', post)">Remove</MyButton>
  </div>
</template>

<script>
  import MyButton from './UI/MyButton.vue';

  export default {
    props: {
      todo: {
        type: Object,
        required: true,
      }
    },
    components: { MyButton }
}
</script>

<style scoped>
  .item {
    display: flex;
    justify-content: space-between;

    border: 1px solid #173f88;
    border-radius: 10px;

    padding: 10px;
    height: 100%;
  }
  .content {
    width: 80%;
    height: 100%;
    word-wrap: break-word;
  }
  .title {
    font-size: 15px;
    text-transform: capitalize;
  }
  .body {
    font-size: 13px;
  }
  .time {
    font-size: 10px;
    font-weight: 600;
  }
</style>