
<script setup>


import {ref} from "vue";


const  BoardWidth=ref(15)
const BoardHeight=ref(15)
const isPlaying=ref(false);

const FirstPlayer=ref('X')
const CurrentPlayer=ref(FirstPlayer.value)
const logicBoard=ref([BoardHeight].map(()=>{[BoardWidth].fill('')}))
function resetGame(){
  if(isPlaying.value){
    alert("Current Game are playing, please finish or dismiss!")
    return
  }
  logicBoard.value=[BoardHeight].map(()=>{[BoardWidth].fill('')})
  CurrentPlayer.value=FirstPlayer.value
}
function handleCellClick(y,x)
{
  if(logicBoard[y][x].value!=='')
  {
    return
  }
  logicBoard[y][x].value=CurrentPlayer.value;
  CurrentPlayer.value=(CurrentPlayer.value==='X'?'O':'X')
}
</script>
<template class="master">
  <div class="LeaderBoard">

  </div>
  <div class="GameBoard">
    <div   v-for="y in logicBoard.value.length" :key="y">
      <div  v-for="x in logicBoard.value[y]" :key="x">
        <div class="game-grid-item" @click="handleCellClick(y,x)">
<!--          {{logicBoard.value[y][x]!==''?logicBoard.value[y][x]:''}}-->
          {{logicBoard.value[y][x]}}
          </div>
        </div>
    </div>
  </div>
  <div class="Setting">
    <div class="grid-item"> Width:  <input type="number" v-model="BoardWidth" min="3" max="25"/></div>
    <div class="grid-item"> Height:  <input type="number" v-model="BoardHeight" min="3" max="25"/></div>
    <div class="grid-item">First Player:
      <select v-model="CurrentPlayer" >
      <option>X</option>
        <option>O</option>
      </select></div>
    <div class="grid-item"><button :disabled="isPlaying" @click="resetGame">Reset</button></div>

  </div>
</template>
<style scoped>
.master{
  display: flex;
  flex-direction: row;
  padding: 20px;
  border-radius: 10px;
  background-color: white;
  min-height: 500px;
}
.LeaderBoard{
  width: 20%;

}
.GameBoard{
  width: 50%;
  display:grid;
  background-color: #f2f2f2;
  padding: 10px;
}
.Setting{
  width: 30%;
  display: grid;
  column-gap:20px;
  row-gap:20px;
}
.grid-item{
  background-color: cyan;
  border: 5px;
}
</style>
