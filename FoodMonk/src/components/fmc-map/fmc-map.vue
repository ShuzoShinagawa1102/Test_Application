<template>
  <view class="map-container">

    <view class="section-title">
      <text class="title-h2">Food monk</text>
    </view>

    <view class="map-component">
      <view id="map_canvas"></view>
    </view>

    <view id="map-list" class="scrollable-list">
    </view>

  </view>
</template>

<script setup lang="ts">
  import { ref } from "vue";
  








</script>

<style scoped>

/* 1. アプリケーションのタイトル "Food monk" */
.section-title {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px 0;
}

.title-h2 {
    font-size: 24px; /* フォントサイズは適宜調整可能 */
    text-align: center;
    font-weight: bold;
}

/* 2. マップのスタイル */
.map-component {
    width: 100%;
    height: 300px; /* スマホで見やすい高さに設定。適宜調整可能 */
    margin-top: 20px;
}
.map-container {
    flex: 1; /* 利用可能なスペースを埋める */
}

#map_canvas {
    width: 100%;
    height: 100%;
    background-color: #e9e9e9; /* マップがロードされるまでの背景色。適宜調整可能 */
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
</style>
