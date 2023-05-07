<script setup>
defineProps({
  disabled: Boolean
})
defineEmits(['delete'])
</script>

<template>
  <button
      class="delete-btn"
      :disabled="disabled"
      @click="$emit('delete')"
  >
    <span class="delete-text">Удалить</span>
    <img src="../assets/images/delete.svg" alt="delete" />
  </button>
</template>

<style scoped>
  .delete-btn {
    width: 100px;
    height: 38px;
    margin-left: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    outline: none;
    background: #E5E5E5;
    transition: .3s;
    cursor: pointer;
  }
  .delete-btn:active {
    background: #cccccc;
  }
  .delete-text {
    font-weight: 400;
    font-size: 13px;
    line-height: 20px;
    color: #000000;
    margin-right: 12px;
  }
  button[disabled] {
    pointer-events: none;
  }
</style>
