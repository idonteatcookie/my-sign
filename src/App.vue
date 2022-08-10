<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import SelectTemplate from './components/SelectTemplate.vue';
import EditContent from './components/EditContent.vue';
import GenerateResult from './components/GenerateResult.vue';
import Button from './components/Button.vue';
import { ref } from 'vue';

const step = ref(0);
const template = ref();
const title = ref();
const result = ref();

const toStep1 = (selectTpl) => {
  template.value = selectTpl;
  step.value = 1;
};
const toStep2 = (editContent) => {
  title.value = editContent.title;
  result.value = editContent.result;
  step.value = 2;
};
</script>

<template>
  <div class="app">
    <div v-if="step === 0">
      <h1 class="step-title">选择模板</h1>
      <SelectTemplate @select="(tpl) => toStep1(tpl)" />
    </div>
    <div v-if="step === 1">
      <EditContent
        :template="template"
        @next="toStep2"
        @prev="step--"
      />
    </div>
    <div v-if="step === 2">
      <div class="button-ops">
        <Button class="btn" @click="step--">返回上一步</Button>
      </div>
      <GenerateResult :result="result" :title="title" />
    </div>
  </div>
</template>

<style scoped>
.app {
  padding: 20px;
  width: 800px;
  margin: 40px auto;
  box-shadow: 1px 1px 5px 2px rgb(0 0 0 / 10%);
  background: #fff;
}
.step-title {
  font-size: 20px;
  font-weight: 500;
}
.button-ops {
  margin-bottom: 10px;
  border-bottom: 1px solid #d7d7d7;
  padding-bottom: 10px;
}
.btn {
  margin-right: 6px;
}
</style>
