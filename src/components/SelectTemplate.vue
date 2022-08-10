<script setup>
import templates from '../constant/templates.js';
const emit = defineEmits(['select']);

const onClick = (tpl) => {
  emit('select', tpl);
};
</script>

<template>
  <div class="select-template">
    <div
      class="template-item"
      v-for="(tpl, index) in templates"
      :key="index"
      @click="onClick(tpl)"
    >
      {{ tpl.title }}
    </div>
  </div>
</template>

<style scoped>
.select-template {
  padding: 20px;
  border: 1px solid #c9c9c9;
}
.template-item {
  padding: 10px;
  cursor: pointer;
}
.template-item:hover {
  text-decoration: underline;
}
</style>
