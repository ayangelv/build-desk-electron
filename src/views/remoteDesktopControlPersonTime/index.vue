<template>
  <div class="content">
    <img
      :src="icon"
      alt=""
      class="icon"
    />
    <div class="text">
      {{ formUserName }} 正在控制你的电脑 {{ formattedTime }}
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, onUnmounted, ref, watchEffect } from 'vue';
import { useRoute } from 'vue-router';
const route = useRoute();

import icon from './icon.png';
const formUserName = ref();

onMounted(() => {
  console.log('route.query', route.query);
  formUserName.value = route.query.formUserName;
  startTimer();
});

const timer = ref(null);
const seconds = ref(0);
const formattedTime = ref('');

// 格式化时间为 mm:ss 格式
const formatTime = (sec) => {
  const minutes = Math.floor(sec / 60)
    .toString()
    .padStart(2, '0');
  const secs = (sec % 60).toString().padStart(2, '0');
  return `${minutes}:${secs}`;
};

// 更新格式化时间
watchEffect(() => {
  formattedTime.value = formatTime(seconds.value);
});

// 开始计时
const startTimer = () => {
  if (timer.value) return; // 防止重复计时
  timer.value = setInterval(() => {
    seconds.value++;
  }, 1000);
};

// 停止计时
const stopTimer = () => {
  if (timer.value) {
    clearInterval(timer.value);
    timer.value = null;
  }
};

// 组件卸载时清理计时器
onUnmounted(() => {
  if (timer.value) {
    clearInterval(timer.value);
  }
});
</script>

<style lang="scss" scoped>
.content {
  height: 40px;
  background-color: #485967;
  -webkit-app-region: drag;
  display: flex;
  align-items: center;
  justify-content: center;
  .text {
    font-size: 14px;
    color: #ffffff;
  }
  .icon {
    width: 12px;
    height: 12px;
    margin-right: 10px;
  }
}
</style>
