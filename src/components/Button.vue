<template>
  <button
    :class="{
      primary: props.type === 'primary',
    }"
  >
    <slot></slot>
  </button>
</template>

<script setup>
const props = defineProps({
  type: String,
});
</script>

<style scoped>
button {
  padding: 6px 12px;
  margin: 0;
  outline: none;
  cursor: pointer;
  border-radius: 4px;
  overflow: hidden;
  position: relative;
  background: #ffffff;
  color: #7f7f7f;
  border: 1px solid;
  font-size: 12px;
}
button.primary {
  border: 1px solid transparent;
  background: #2498ff;
  color: #fff;
}
button:active::after {
  display: block;
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.05);
}
</style>
