<script setup>

import {ref} from "vue";

const winnerName=ref('')
</script>

<template>
<div class="modal-backdrop" @click.self="this.$emit('close')">
  <div class="modal-content">
    <h2> Congratulation! You have won!</h2>
    <p> Please insert your name:</p>
    <input :style="{margin:'10px',borderRadius: '10px',textAlign:'center', backgroundColor:'coral'}" v-model="winnerName" placeholder="e.g: Tommy" style="min-width: 200px" @keyup.enter="$emit('addWinnerName',winnerName)">
    <button :style="{borderRadius:'10px', backgroundColor:'yellowgreen'}" @click="$emit('addWinnerName',winnerName)">Finish</button>
  </div>
</div>
</template>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center; /* Horizontally centers the modal */
  align-items: center;     /* Vertically centers the modal */
  z-index: 1000; /* Ensures it is above other content */
}
.modal-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 500px;
  height: 200px;
  background-color: cornflowerblue;
  border-radius: 10px;
  color: yellowgreen;
}
</style>