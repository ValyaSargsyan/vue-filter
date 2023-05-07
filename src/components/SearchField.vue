<script setup>

defineProps({
    modelValue: String,
})
defineEmits(['update:modelValue'])
</script>

<template>
  <div class="input-wrap">
    <img src="../assets/images/search.svg" alt="search" class="search-icon">
    <input
        :value="modelValue"
        placeholder="Введите ЖК / корпус / № квартиры / № паркинга"
        class="search-input"
        @input="$emit('update:modelValue', $event.target.value)"
    />
  </div>

</template>

<style scoped>
  .input-wrap {
    position: relative;
    margin-bottom: 30px;
  }
  .search-input {
    width: 100%;
    height: 38px;
    background: #F7F6F4;
    border: 1px solid #C4C4C4;
    padding-left: 100px;
    font-weight: 400;
    font-size: 14px;
    line-height: 18px;
    outline: none;
  }
  .search-input::placeholder {
    color: #9B9B9B;
  }

  .search-icon {
    position: absolute;
    left: 34px;
    top: 50%;
    transform: translateY(-50%);
  }

  @media(max-width: 1280px) {
    .search-input {
      padding-left: 72px;
    }
    .search-icon {
      left: 23px;
    }
  }
  @media(max-width: 768px) {
    .input-wrap {
      margin-bottom: 25px;
    }
    .search-input {
      padding-left: 35px;
    }
    .search-icon {
      left: 8px;
    }
  }
</style>
