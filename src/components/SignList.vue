<script setup>
import { ref } from 'vue';
import signs from '../constant/signs.js';
import SignTag from './SignTag.vue';
const props = defineProps({
  usedList: Array,
  selectItem: Object,
});
const emit = defineEmits(['select-change']);

const tagList = ref(
  signs.map((item, index) => {
    return {
      ...item,
    };
  })
);

const onChange = (value, selectItem) => {
  emit('select-change', value ? selectItem : null);
};
</script>

<template>
  <div class="sign-list">
    <SignTag
      v-for="item in tagList"
      :key="item.nameEn"
      :select="props.selectItem === item"
      :disabled="props.usedList.includes(item.nameEn)"
      selectable
      @change="onChange($event, item)"
      :sign-item="item"
      class="tag-item"
    />
  </div>
</template>

<style scoped>
.sign-list {
  display: flex;
  flex-wrap: wrap;
  padding-left: 20px;
  border-bottom: 1px solid #c9c9c9;
}
.tag-item {
  margin-right: 10px;
  margin-bottom: 10px;
}
</style>
