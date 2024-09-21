
<script setup>


import {computed, ref} from "vue";


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
    {{LeaderBoardDataAmount===0?'No record':LeaderBoardDataAmount}}
    <li :style="{display:'flex', justifyContent:'center'}" v-if="LeaderBoardData.length>0" v-for="(name,index) in LeaderBoardData" :key="index">
      Game {{index}}: <br> name
    </li>

  </div>
  <div class="GameBoard">

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
  background-color: yellow;
}
.GameBoard{
  width: 50%;
  min-height: 300px;
  display:flex;
  background-color: yellow;
  padding: 10px;
  border-radius: 20px;
  margin: 20px;

}
.GameBoardRow{
  flex-direction: row;
}
.GameBoardCell{
  background-color: yellow;
  border-radius: 10px;
}

.Setting{
  width: 30%;
  display: grid;
  column-gap:20px;
  row-gap:20px;
  border-radius: 20px;
  margin: 20px;
  background-color: yellow;
}

</style>
