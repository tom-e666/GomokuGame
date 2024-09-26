
<script setup>

import {computed, ref, watch} from "vue";
const  BoardWidth=ref(4)
const BoardHeight=ref(5)
const isPlaying=ref(false);
const FirstPlayer=ref('X')
const CurrentPlayer=ref(FirstPlayer.value)
const logicBoard=ref(Array(BoardHeight.value).fill(null).map(()=>(Array(BoardWidth.value).fill(null))))
watch(logicBoard,()=>{console.log(logicBoard.value)})
function resetGame(){
  if(isPlaying.value){
    alert("Current Game are playing, please finish or dismiss!")
    return
  }
  logicBoard.value=Array(BoardHeight.value).fill(null).map(()=>(Array(BoardWidth.value).fill(null)))
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
const LeaderBoardData=ref([
])
const LeaderBoardDataAmount=computed(()=>{
  return LeaderBoardData.value.length
})
</script>
<template>
  <div class="master">
  <div class="LeaderBoard">
    <h3 :style="{display:'flex',justifyContent:'center'}">LEADER BOARD</h3>
    <div v-if="LeaderBoardDataAmount===0" :style="{display:'flex', justifyContent:'center', alignItems:'center', height:'100%'}">No Record</div>
    <div v-else :style="{display:'flex', justifyContent:'center'}" v-for="(name,index) in LeaderBoardData" :key="index">
      Game {{index}}: <br> {{name}}
    </div>

  </div>
  <div class="GameBoard">
    <div v-for="(row,y) in logicBoard" :key="y" class="GameBoardRow">
      <div v-for="(cell,x) in logicBoard[y]" :key="x"
           class="GameBoardCell"
           @click="handleCellClick(y,x)"
      >
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
  </div>
</template>
<style scoped>
.master{
  display: flex;
  flex-direction: row;
  min-height: 500px;
}
.LeaderBoard{
  display:block;
  width: 20%;
  border-radius: 20px;
  margin: 20px;
  background-color: gray;
}
.GameBoard{
  width: 50%;
  min-height: 300px;
  display:flex;
  flex-direction: column;
  background-color: gray;
  padding: 10px;
  border-radius: 20px;
  margin: 20px;
  justify-content: center;
  align-items: center;
}
.GameBoardRow{
  display: flex;
  flex-direction: row;
}
.GameBoardCell{
  min-width: 30px;
  min-height:30px;
  border-radius:10px;
  margin: 1px;
  background-color: white;
}

.Setting{
  width: 30%;
  display: grid;
  column-gap:20px;
  row-gap:20px;
  border-radius: 20px;
  margin: 20px;
  background-color: gray;
}

</style>
