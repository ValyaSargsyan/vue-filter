<script setup>

import {computed} from "vue";

const props = defineProps({
  modelValue: Boolean,
  label: String,
})
const emits = defineEmits(['update:modelValue', 'change'])

const model = computed( {
  get() {
    return props.modelValue;
  },
  set(value) {
    emits('update:modelValue', value)
  },
})

</script>

<template>
  <label class="container" >
    <span class="label">{{label}}</span>
    <input
        type="checkbox"
        v-model="model"
        @change="emits('change')"
    >
    <span class="checkmark"></span>
  </label>
</template>

<style scoped>

.label {
  font-weight: 400;
  font-size: 13px;
  line-height: 20px;
  color: #000000;
  display: block;
  margin: -4px 0 0 0;
}

.container {
  display: block;
  position: relative;
  padding-left: 25px;
  height: 16px;
  cursor: pointer;
  font-size: 13px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 16px;
  width: 16px;
  border: 1px solid #C4C4C4;
  background-color: transparent;
}

.container:hover input ~ .checkmark {
  background-color: #dcdcdc;
}

.container input:checked ~ .checkmark {
  background-color: #FCE66F;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.container input:checked ~ .checkmark:after {
  display: block;
}

.container .checkmark:after {
  left: 5px;
  top: 0;
  width: 5px;
  height: 10px;
  border: solid #000000;
  border-width: 0 1px 1px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
