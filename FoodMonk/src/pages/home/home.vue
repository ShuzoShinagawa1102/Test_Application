<template>
  <view class="container">
    <fmc-header />
    <fmc-map />
    <fmc-footer />
  </view>
</template>

<script setup lang="ts">
  import { ref } from "vue";
</script>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}
.map-container {
    flex: 1;
}
.footer-wrapper {
    width: 100%;
}

</style>

