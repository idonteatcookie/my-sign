<script setup>
import { ref } from 'vue';
import { computed } from '@vue/reactivity';
import draggable from 'vuedraggable';
import SignList from './SignList.vue';
import SignTag from './SignTag.vue';
import Input from './Input.vue';
import Button from '../components/Button.vue';
import signs from '../constant/signs.js';
const props = defineProps({
  template: Object,
});
const emit = defineEmits(['next', 'prev']);
const title = ref(props.template.title);
const result = ref(
  props.template.content.map((item, index) => {
    const sign = signs.find((sign) => sign.name === item.name);
    return {
      sign,
      desc: item.desc,
      key: index,
    };
  })
);
defineExpose({
  result,
});
const usedList = computed(() => {
  return result.value
    .filter((item) => item.sign)
    .map((item) => item.sign.nameEn);
});
const selectItem = ref(null);
const onSelectChange = (item) => {
  selectItem.value = item;
};
const onSelect = (element) => {
  if (selectItem.value) {
    element.sign = selectItem.value;
    selectItem.value = null;
  }
};
const onDelete = (element) => {
  element.sign = null;
};
const next = () => {
  if (usedList.value.length !== 12) {
    alert('请把所有星座都选齐哦！');
    return;
  }
  emit('next', { title: title.value, result: result.value });
};
</script>

<template>
  <div class="sign-wrapper">
    <div class="button-ops">
      <Button class="btn" @click="emit('prev')">返回上一步</Button>
      <Button class="btn" @click="next" type="primary">下一步</Button>
    </div>
    <div class="title">
      <label class="title-label">标题</label>
      <Input v-model="title" :style="{ height: '30px' }"></Input>
    </div>
    <SignList
      @select-change="onSelectChange"
      :select-item="selectItem"
      :used-list="usedList"
    />
    <draggable
      v-model="result"
      ghost-class="ghost"
      dragClass="drag"
      handle=".sign-drag"
      item-key="key"
    >
      <template #item="{ element }">
        <div class="sign-item">
          <div class="sign-drag">
            <i class="iconfont icon-drag"></i>
          </div>
          <div class="selected-sign">
            <SignTag
              @click="onSelect(element)"
              v-if="!element.sign"
              label="未选择"
              disabled
              style="width: 100%"
            />
            <SignTag
              closeable
              @close="onDelete(element)"
              v-else
              :sign-item="element.sign"
            />
          </div>
          <div class="sign-desc">
            <Input v-model="element.desc" />
          </div>
        </div>
      </template>
    </draggable>
  </div>
</template>

<style scoped>
.sign-wrapper {
}

.sign-item {
  padding: 10px 20px 10px 0;
  display: flex;
  font-size: 14px;
  border-bottom: 1px solid #ededed;
  background: #fff;
  align-items: center;
}

.sign-drag {
  width: 20px;
  text-align: center;
  cursor: move;
  margin-right: 10px;
}

.selected-sign {
  flex: 86px 0 0;
  margin-right: 6px;
  display: flex;
}
.sign-icon {
  margin-right: 4px;
}

.sign-desc {
  flex: 100px 1 0;
}

.ghost {
  background: #ffdbdb;
}

.drag {
  background: rgba(255, 255, 255, 0.9);
}
.button-ops {
  margin-bottom: 10px;
  border-bottom: 1px solid #d7d7d7;
  padding-bottom: 10px;
}
.btn {
  margin-right: 6px;
}
.title {
  display: flex;
  border-bottom: 1px solid #d7d7d7;
  padding-bottom: 10px;
  margin-bottom: 10px;
  font-size: 14px;
}
.title-label {
  flex: 40px 0 0;
}
</style>
