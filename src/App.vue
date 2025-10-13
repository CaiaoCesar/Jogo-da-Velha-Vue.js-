<template>
  <HeaderInfo></HeaderInfo>
  <ImagesGame></ImagesGame>

  <!-- GameBoard emite o evento game-ended -->
  <GameBoard @game-ended="handleGameEnd"></GameBoard>

  <!-- ScoreTable com ref para podermos acessar seus métodos -->
  <ScoreTable ref="scoreTable"></ScoreTable>

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
  },
  methods: {
    handleGameEnd(result) {
      // Chama o método updateScore do ScoreTable
      this.$refs.scoreTable.updateScore(result);
    }
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  background-color: #333; 
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2a94a6ff;
  margin-top: 20px;
  background-color: #333;
}
</style>