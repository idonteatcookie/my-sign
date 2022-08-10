<script setup>
import { computed } from '@vue/reactivity';

const props = defineProps({
  closeable: Boolean,
  select: Boolean,
  disabled: Boolean,
  selectable: Boolean,
  signItem: Object,
  label: String,
});
const emit = defineEmits(['close', 'change']);
const selectable = computed(() => props.selectable && !props.disabled);

const onClose = () => {
  emit('close');
};
const onClick = () => {
  if (selectable.value) {
    emit('change', !props.select);
  }
};
</script>

<template>
  <div
    class="sign-tag"
    :class="{
      select: props.select && !props.disabled,
      disabled: props.disabled,
    }"
    :style="{ cursor: selectable ? 'pointer' : '' }"
    @click="onClick"
    v-if="props.signItem"
  >
    <div class="sign-info">
      <div class="sign-icon">{{ props.signItem.icon }}</div>
      <div class="sign-cn">{{ props.signItem.name }}</div>
    </div>
    <span class="close-btn" v-if="closeable" @click="onClose">
      <i class="iconfont icon-closefill"></i>
    </span>
  </div>

  <div class="sign-tag label" v-else>
    <div class="label">{{ props.label }}</div>
  </div>
</template>

<style scoped>
.sign-tag {
  padding: 4px 12px;
  font-size: 14px;
  position: relative;
  border-radius: 4px;
  background: #d8f4ff;
  color: #7a7a7a;
  border: 1px solid transparent;
  line-height: 20px;
  text-align: center;
}
.sign-tag.select {
  background: #ffb033;
  color: #ffffff;
  border: 1px solid transparent;
}
.sign-tag.disabled {
  color: #b0b0b0;
  border: 1px dashed;
  background: #fff;
  cursor: not-allowed;
}
.sign-tag.label {
  color: #b0b0b0;
  border: 1px dashed;
  background: #fff;
  cursor: pointer;
  text-align: center;
}
.sign-info {
  display: flex;
}
.sign-icon {
  margin-right: 4px;
}
.close-btn {
  position: absolute;
  top: -6px;
  right: -6px;
  color: #fff;
  color: red;
  cursor: pointer;
}
</style>
