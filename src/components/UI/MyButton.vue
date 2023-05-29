<template>
  <button>
    <slot></slot>
  </button>
</template>

<script setup>

</script>

<style scoped>
  button {
    margin-top: 10px;
    align-self: flex-end;
    padding: 10px 15px;
    background: none;
    color: brown;
    border: 1px solid brown;
  }
</style>