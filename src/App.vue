<script setup>
import BannerComponent from "@/components/BannerComponent.vue";
import GomokuGame from "@/components/GomokuGame.vue";
</script>
<template>
  <div class="container">
    <BannerComponent/>
      <GomokuGame/>
  </div>
</template>
<style>
.container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>