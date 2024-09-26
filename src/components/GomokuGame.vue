
<script setup>

import {computed, nextTick, ref, watch} from "vue";
import ModalVictoryAlert from "@/components/ModalVictoryAlert.vue";
const isVisibleModalVictoryAlert = ref(false);
const  BoardWidth=ref(15)
const BoardHeight=ref(15)
const isPlaying=ref(false);
const FirstPlayer=ref('X')
const CurrentPlayer=ref(FirstPlayer.value)
const logicBoard=ref(Array(BoardHeight.value).fill(null).map(()=>(Array(BoardWidth.value).fill(null))))
const winCondition=ref(3)
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
  if(logicBoard.value[y][x]!==null)
  {
    return
  }
  logicBoard.value[y][x]=CurrentPlayer.value;
  nextTick(()=>{
    handleGameLogic(y,x);
    CurrentPlayer.value=(CurrentPlayer.value==='X'?'O':'X')
  })
}
function handleGameLogic(y, x) {
  const yFix = y;
  const xFix = x;
  const curr = logicBoard.value[yFix][xFix]; // Current player's move

  const dy = [0, -1, -1, -1];
  const dx = [1, 1, 0, -1];

  for (let i = 0; i < 4; ++i) {
    let count = 1;
    while (
        y + dy[i] >= 0 && y + dy[i] < logicBoard.value.length &&
        x + dx[i] >= 0 && x + dx[i] < logicBoard.value[y].length &&
        logicBoard.value[y + dy[i]][x + dx[i]] === curr
        ) {
      count++;
      y += dy[i];
      x += dx[i];
    }
    y = yFix;
    x = xFix;
    while (
        y - dy[i] >= 0 && y - dy[i] < logicBoard.value.length &&
        x - dx[i] >= 0 && x - dx[i] < logicBoard.value[y].length &&
        logicBoard.value[y - dy[i]][x - dx[i]] === curr
        ) {
      count++;
      y -= dy[i];
      x -= dx[i];
    }

    if (count >= winCondition.value) {
      handleVictory();
      return;
    }
    y = yFix;
    x = xFix;
  }
}

function handleVictory(){
  console.log('handleVictory()')
  alert(`${CurrentPlayer.value} has won!`)
  isVisibleModalVictoryAlert.value=true
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
    <h3 :style="{display:'flex',justifyContent:'center',fontWeight:'bold',margin:'20px 0px'}">LEADERBOARD</h3>
    <div v-if="LeaderBoardDataAmount===0" :style="{display:'flex', justifyContent:'center', alignItems:'center', height:'100%'}">No Record</div>
    <p v-else :style="{display:'flex', justifyContent:'center'}" v-for="(name,index) in LeaderBoardData" :key="index">
     {{name}}
    </p>

  </div>
  <div class="GameBoard">
    <div v-for="(row,y) in logicBoard" :key="y" class="GameBoardRow">
      <div v-for="(cell,x) in logicBoard[y]" :key="x"
           class="GameBoardCell"
           @click="handleCellClick(y,x)"
           :style="{color:cell==='X'?'#4caf50':'#2196f3',fontWeight:'bolder'}"
      >
        {{cell}}
      </div>
    </div>
    </div>

  <div class="Setting">
    <p class="setting-item"> Width:</p> <input class="setting-item" type="number" v-model="BoardWidth" min="3" max="25"/>
    <p class="setting-item"> Height:</p> <input class="setting-item" type="number" v-model="BoardHeight" min="3" max="25"/>
    <p class="setting-item">Win condition:</p> <input class="setting-item" :disabled="isPlaying" type="number" v-model="winCondition" :min="3" :max="Math.max(BoardWidth, BoardHeight)"/>
    <p class="setting-item">First Player:</p>
      <select class="setting-item" v-model="FirstPlayer" :disabled="isPlaying" >
        <option>X</option>
        <option>O</option>
      </select>
    <p class="setting-item">Reset Game</p> <button class="setting-item" :disabled="isPlaying" @click="resetGame">Reset</button>
  </div>
    <ModalVictoryAlert v-if="isVisibleModalVictoryAlert"
                       @close="isVisibleModalVictoryAlert=false"
                        @addWinnerName="(winnerName)=>{isVisibleModalVictoryAlert=false; LeaderBoardData.push(winnerName===''?'Anonymous':winnerName)}"/>
  </div>
</template>
<style scoped>
.master{
  width: 100%;
  display: flex;
  flex-direction: row;
  min-height: 500px;
}
.LeaderBoard{
  display:block;
  width: 20%;
  border-radius: 20px;
  margin: 20px;
  background-color: coral;
  color: purple;
}
.GameBoard{
  width: 50%;
  min-height: 300px;
  display:flex;
  flex-direction: column;
  background-color: coral;

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
  display: flex;
  min-width: 30px;
  min-height:30px;
  border-radius:10px;
  margin: 1px;
  background-color: white;
  align-items: center;
  justify-content: center;
  color: #181818;
  cursor: pointer;
  caret-color: transparent;
}
.Setting{
  width: 30%;
  display: grid;
  grid-template-columns: 2fr 1fr;
  column-gap:20px;
  row-gap:20px;
  border-radius: 20px;
  margin: 20px;
  background-color: coral;
}
.setting-item{
  display: flex;
  justify-content: left;
  align-items: center;
  left: 10px;
  margin: 10px;
}
input,select,button{
border-radius: 10px;
  background-color: greenyellow;
  text-align: center;
  height: 40px;
}
p{
  font-weight: bolder;
  color: greenyellow;
}
</style>
