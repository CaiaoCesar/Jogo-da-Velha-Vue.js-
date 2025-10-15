<template>
  <HeaderInfo></HeaderInfo>
  <ImagesGame></ImagesGame>

  <!-- ScoreTable emite os nomes dos jogadores -->
  <ScoreTable ref="scoreTable" @player-names-updated="handlePlayerNamesUpdate"></ScoreTable>

  <!-- GameBoard recebe os nomes dos jogadores -->
  <GameBoard @game-ended="handleGameEnd" :playerNames="playerNames"></GameBoard>

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
  data() {
    return {
      playerNames: {
        playerX: "Jogador 1",
        playerO: "Jogador 2"
      }
    }
  },
  methods: {
    handleGameEnd(result) {
      this.$refs.scoreTable.updateScore(result);
    },

    handlePlayerNamesUpdate(names) {
      // Atualiza os nomes dos jogadores quando são modificados no ScoreTable
      this.playerNames = names;
    }
  }
}
</script>

<style>
html,
body {
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