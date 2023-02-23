<script setup>
import TopImg from "./../assets/topImage.png";
</script>
<template>
  <header>
    <img :src="TopImg" alt="トップ画像" class="topimg" />
  </header>
</template>

<style scoped>
.topimg {
  margin: 20px auto;
  max-height: 70px;
}
</style>
