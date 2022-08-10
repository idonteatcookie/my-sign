<template>
  <textarea class="input" :value="props.modelValue" @input="onInput" />
</template>

<script setup>
const props = defineProps({
  modelValue: String,
});
const emit = defineEmits(['update:modelValue']);

const onInput = (e) => {
  const value = e.target.value;
  emit('update:modelValue', value);
};
</script>

<style scoped>
.input {
  padding: 0 6px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 100%;
  height: 30px;
  outline: none;
  caret-color: #999;
  color: #5b5b5b;
  position: relative;
  font-size: 12px;
  vertical-align: -5px;
}
</style>
