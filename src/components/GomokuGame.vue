
<script setup>


import {computed, ref} from "vue";


const  BoardWidth=ref(15)
const BoardHeight=ref(15)
const isPlaying=ref(false);

const FirstPlayer=ref('X')
const CurrentPlayer=ref(FirstPlayer.value)
const BoardCellValue='X'|'O'|null
const temRow=Array(BoardWidth).fill(null)
const logicBoard= Array(BoardHeight).fill(temRow)
function resetGame(){
  if(isPlaying.value){
    alert("Current Game are playing, please finish or dismiss!")
    return
  }
  logicBoard.value.forEach((col)=>{
    col.forEach((row)=>{
      logicBoard.value[col][row]=null;
    })
  })
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
const LeaderBoardData=ref([
])
const LeaderBoardDataAmount=computed(()=>{
  return LeaderBoardData.value.length
})
console.log(logicBoard.value)
</script>
<template>
  <div class="master">
  <div class="LeaderBoard">
    <h3 :style="{display:'flex',justifyContent:'center'}">LEADER BOARD</h3>
    <div v-if="LeaderBoardDataAmount===0" :style="{display:'flex', justifyContent:'center', alignItems:'center', height:'100%'}">No Record</div>
    <li v-else :style="{display:'flex', justifyContent:'center'}" v-for="(name,index) in LeaderBoardData" :key="index">
      Game {{index}}: <br> name
    </li>

  </div>
  <div class="GameBoard">
    <div v-for="y in logicBoard" :key="y">
      <div v-for="x in logicBoard[y]" :key="x">
1
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
  flex-direction: row;
  background-color: gray;
  padding: 10px;
  border-radius: 20px;
  margin: 20px;

}
.GameBoardRow{
  flex-direction: row;
}
.GameBoardCell{
  min-width: 10px;
  min-height:10px;
  border-radius:10px;
  margin: 10px;
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
