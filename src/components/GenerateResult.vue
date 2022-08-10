<template>
  <div class="config">
    <div class="config-item">
      <label>选择背景色</label><input type="color" v-model="bgColor" />
    </div>
    <div class="config-item">
      <label>选择文字颜色</label><input type="color" v-model="color" />
    </div>
    <div class="config-item">
      <label>选择边框颜色</label><input type="color" v-model="bdColor" />
    </div>
    <div class="config-item">
      <label>选择边框宽度</label>
      <input type="range" :min="0" :max="20" v-model="bdWidth" />
    </div>
  </div>
  <div class="config">
    <div class="config-item">
      <label>选择宽度</label>
      <input type="range" :min="300" :max="760" v-model="width" />
    </div>
    <div class="config-item">
      <label>水印</label>
      <input v-model="watermark" />
    </div>
    <div class="config-item">
      <label>水印颜色</label>
      <input type="color" v-model="watermarkColor" />
    </div>
  </div>

  <div
    class="generate-result"
    :style="{
      background: bgColor,
      color: color,
      borderColor: bdColor,
      width: width + 'px',
      borderWidth: bdWidth + 'px',
    }"
  >
    <h4 class="title">{{props.title}}</h4>
    <div v-for="item in props.result" :key="item.index" class="sign-item">
      <span class="icon">{{ item.sign.icon }}</span>
      <span>{{ item.sign.name }}：</span>
      <span>{{ item.desc }}</span>
    </div>
    <div class="watermark" :style="{color: watermarkColor}">{{watermark}}</div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const props = defineProps({
  result: Object,
  title: String
});
const bgColor = ref('#333333');
const color = ref('#ffffff');
const bdColor = ref('#ff8c8c');
const width = ref(500);
const bdWidth = ref(10);
const watermark = ref('@星座研究院');
const watermarkColor = ref('#696969');
</script>

<style scoped>
.generate-result {
  border: 10px solid;
  padding: 20px;
  border-radius: 2px;
  margin: 0 auto;
  position: relative;
}
.title {
  margin: 0 0 20px 0;
}
.sign-item {
  font-size: 14px;
  margin-bottom: 10px;
}

.icon {
  margin-right: 2px;
}
.config {
  display: flex;
  margin-bottom: 10px;
  align-items: center;
}

.config label {
  margin-right: 4px;
}

.config-item {
  margin-right: 16px;
}
.watermark {
    position: absolute;
    bottom: 10px;
    right: 20px;
    font-size: 16px;
    user-select: none;
}
</style>
