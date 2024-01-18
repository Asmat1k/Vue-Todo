<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
  export default {
    name: 'MyButton',
  };
</script>

<style scoped>
  .btn {
    background-color: transparent;
    border: 1px solid #173f88;
    border-radius: 10px;

    text-transform: uppercase;
    font-weight: 700;
    color: #173f88;

    padding: 5px;
  }
  .btn:hover {
    cursor: pointer;
    
    background-color: #173f88;
    color: white;
  }
</style>
