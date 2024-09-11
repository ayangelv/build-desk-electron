<template>
  <div class="footer">
    <div class="footer-btn-group">
      <!-- <div class="btn-item">
        <div class="btn-item-icon">
          <img
            :src="iconMicroClose"
            alt=""
          />
        </div>
        <div class="btn-item-text">开启麦克风</div>
      </div> -->
      <div
        class="btn-item"
        @click="endRemote"
      >
        <div class="btn-item-icon btn-item-icon--close">
          <img
            :src="iconClose"
            alt=""
          />
        </div>
        <div class="btn-item-text">结束</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue';
import iconClose from './close.png';
onMounted(() => {});

const endRemote = () => {
  console.log('handleWinClosehandleWinClose');
  // 给握信远程主窗口发关闭通知   1步
  window.electronAPI.ipcRenderer.send(
    'handleWinCloseRemoteDesktopControlPerson1'
  );

  // 被控人关闭的时候也要通知主窗口关闭控制人的窗口 1步完成
  // window.electronAPI.ipcRenderer.send('childWindowClose');
};
</script>

<style lang="scss" scoped>
.footer {
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 240px;
  background-color: #485967;
  -webkit-app-region: drag;

  .footer-btn-group {
    display: flex;
    align-items: center;
    justify-content: center;

    .btn-item {
      margin-left: 40px;
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
      padding-bottom: 24px;
      -webkit-app-region: no-drag;

      &:first-child {
        margin-left: 0;
      }

      &-icon {
        width: 40px;
        height: 40px;
        border-radius: 8px;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: rgba(0, 0, 0, 0.3);
        cursor: pointer;

        &.active {
          background-color: #67c23a;
        }

        img {
          height: 24px;
        }
        &--close {
          background-color: #ff5752;

          img {
            height: 20px;
          }
        }
      }

      &-text {
        text-align: center;
        width: 100px;
        position: absolute;
        bottom: 0;
        color: #ffffff;
        font-size: 12px;
      }
    }
  }
}
</style>
