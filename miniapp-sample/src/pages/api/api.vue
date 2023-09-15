<template>
  <view class="content">
    <button type="primary" @click="handleClick(item.url)" v-for="item in list" :key="item.url">{{ item.title }}</button>
  </view>
  <page-navbar :current="3" @clickBarItem="redirectToByIndex" />
</template>

<script setup lang="ts">
const list = [{
  title: '生体認証Sample',
  url: './soterAuthentication'
}]

const handleClick = (url) => {
  uni.navigateTo({ url })
}

const redirectToByIndex = (path: string) => {
  uni.reLaunch({
    url: path,
  });
};
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