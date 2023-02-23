<script setup>
import TopImg from "./../assets/TopImg.png";
</script>
<template>
  <header>
    <img :src="TopImg" alt="トップ画像" class="topImg pt-2" />
  </header>
</template>

<style scoped>
.topImg {
  margin: 20px auto;
  max-height: 70px;
}
</style>
