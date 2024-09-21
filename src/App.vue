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
  display: block;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  min-width: 1000px;
}
</style>