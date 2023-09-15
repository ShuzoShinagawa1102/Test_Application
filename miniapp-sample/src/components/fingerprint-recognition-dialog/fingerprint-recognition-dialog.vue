<template>
  <view v-if="show" class="dialog-shadow">
    <view class="dialog-view">
      <view class="dialog-title">画面ロックの解除</view>
      <view class="dialog-second-title">指紋認証をおこなってください。</view>
      <view class="dialog-content">
        <image v-if="type === 'Info'" class="dialog-content-image" src="/static/info.png" />
        <image v-if="type === 'Error' || type === 'SystemLock' || type === 'Unsupported'" class="dialog-content-image" src="/static/error.png" />
        <image v-if="type === 'Success'" class="dialog-content-image" src="/static/success.png" />
        <view v-if="type === 'Info'" class="dialog-content-text-info">センサーに触ってください。</view>
        <view v-if="type === 'Error'" class="dialog-content-text-error">指紋認征が失敗しました。<br />もうー度行ってください。</view>
        <view v-if="type === 'SystemLock'" class="dialog-content-text-error">システムはロックされています。<br />デバイスのロックを解除してから再度お試しください。</view>
        <view v-if="type === 'Unsupported'" class="dialog-content-text-error">システムは生体認証をサポートしていません<br />ご確認ください</view>
        <view v-if="type === 'Success'" class="dialog-content-text-success">指紋認証が成功しました。<br />画面ロックを解除します。</view>
      </view>
      <view class="dialog-cancel" @click="handleCancel">キャンセル</view>
    </view>
  </view>
</template>

<script setup lang="ts">
defineProps({
  type: {
    type: String,
    default: 'Info'
  },
  show: {
    type: Boolean,
    required: true
  }
})

const emit = defineEmits([
  "handleCancel",
  "update:show"
]);

const handleCancel = () => {
  emit("handleCancel");
  emit("update:show", false);
};
</script>

<style>
.dialog-shadow {
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  padding: 60px 0;
  background: rgba(7, 0, 0, 0.4);
  overflow-y: auto;
  z-index: 4;
  pointer-events: initial;
}

.dialog-view {
  background: #ffffff;
  color: #000;
  position: relative;
  margin: 10px auto 70px;
  padding: 15px 24px 12px;
  width: calc(100vw - 100px);
  min-width: 267px;
  font-size: 0;
  border-radius: 3px;
  box-shadow: 0px 3px 20px 0.3px rgba(0, 0, 0, 0.1);
  pointer-events: initial;
}

.dialog-title {
  font-size: 22px;
}

.dialog-second-title {
  padding: 15px 0;
  font-size: 17px;
}

.dialog-content {
  margin: 10px 0 20px;
}

.dialog-content-image {
  display: inline-block;
  margin-right: 15px;
  width: 50px;
  height: 50px;
  vertical-align: middle;
}

.dialog-content-text-info {
  display: inline-block;
  padding-bottom: 2px;
  max-width: 200px;
  font-size: 15px;
  vertical-align: middle;
  color: #777;
}

.dialog-content-text-error {
  display: inline-block;
  padding-bottom: 2px;
  max-width: 200px;
  font-size: 15px;
  vertical-align: middle;
  color: #ef403c;
}

.dialog-content-text-success {
  display: inline-block;
  padding-bottom: 2px;
  max-width: 200px;
  font-size: 15px;
  vertical-align: middle;
  color: #2594af;
}

.dialog-cancel {
  margin-bottom: 10px;
  font-size: 16px;
  text-align: right;
  color: #2594af;
}
</style>
