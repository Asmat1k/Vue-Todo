<template>
  <div>
    <div>Title:{{ todo.title }}</div>
    <div>Text:{{ todo.body }}</div>
    <div>Time: {{ todo.time }}</div>
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

<style>
  
</style>