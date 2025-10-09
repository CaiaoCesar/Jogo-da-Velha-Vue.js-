<template>
  <HeaderInfo></HeaderInfo>
  <ImagesGame></ImagesGame>
  <GameBoard></GameBoard>
  <ScoreTable></ScoreTable>
  <GameInstructions></GameInstructions>
</template>

<script>
import GameBoard from './components/GameBoard.vue'
import HeaderInfo from './components/HeaderInfo.vue';
import ScoreTable from './components/ScoreTable.vue';
import GameInstructions from './components/GameInstructions.vue';
import ImagesGame from './components/ImagesGame.vue';

export default {
  name: 'App',
  components: {
    ImagesGame,
    GameBoard,
    HeaderInfo,
    ScoreTable,
    GameInstructions
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2a94a6ff;
  margin-top: 20px;
  background-color: #333;
  padding: 0 20px;
}

</style>
