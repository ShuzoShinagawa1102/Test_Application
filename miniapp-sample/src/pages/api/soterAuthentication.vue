<template>
  <view class="content">
    <button type="primary" @click="handleClick">生体認証をオンにする</button>
  </view>
  <fingerprint-recognition-dialog v-model:show="show" :type="type" @handleCancel="cancel" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import mini from "@/mini";

const show = ref(false)

const type = ref<"Info" | "Success" | "Error" | "SystemLock" | "Unsupported">("Info");

let soterAuthentication: { cancel: () => void; }

// let timer

const handleClick = () => {
  soterAuthentication = mini.soterAuthentication({
    onStart: (soterType) => {
      if (plus.os.name?.toLowerCase() === 'android') {
        // timer = setTimeout(() => {
        //   cancel()
        // }, 10000);
        show.value = true
        type.value = "Info"
      }
    },
    onSuccess: (soterType) => {
      if (plus.os.name?.toLowerCase() === 'android') {
        type.value = "Success"
        show.value = false
      }
      uni.navigateTo({ url: './soterAuthenticationSuccess' })
      plus.nativeUI.toast(soterType)
    },
    onError: (errCode) => {
      if (plus.os.name?.toLowerCase() === 'android') {
        plus.nativeUI.toast(errCode)
        if (errCode === 'SystemLock') {
          type.value = 'SystemLock'
          return
        }
        if (errCode === 'Unsupported') {
          type.value = 'Unsupported'
          return
        }
        if (errCode === 'AuthenticationFailed') {
          type.value = 'Error'
          return
        }
        if (errCode === 'Cancel') {
          show.value = false
          // if (timer) clearTimeout(timer)
        }
        type.value = "Error"
      }
    }
  })
}

const cancel = () => {
  if (soterAuthentication) {
    soterAuthentication.cancel()
  }
  // if (timer) clearTimeout(timer)
  show.value = false
}
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: calc(100vh - 100px);
}

.content button {
  margin-top: 7px;
  margin-bottom: 1px;
  width: 75%;
}
</style>