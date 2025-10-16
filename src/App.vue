<template>
  <div class="app-container">
    <HeaderInfo></HeaderInfo>
    <ImagesGame></ImagesGame>

    <div class="main-game-area">
      <div class="score-section">
        <ScoreTable ref="scoreTable" @player-names-updated="handlePlayerNamesUpdate"></ScoreTable>
      </div>

      <div class="game-section">
        <GameBoard @game-ended="handleGameEnd" :playerNames="playerNames" @reset-game="handleResetGame"></GameBoard>
      </div>
    </div>

    <GameInstructions></GameInstructions>
  </div>
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
      this.playerNames = names;
    },

    handleResetGame() {
      this.$refs.scoreTable.resetScore();
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  margin: 0;
  padding: 0;
  background-color: #333;
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2a94a6ff;
  background-color: #333;
  min-height: 100vh;
}

.app-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  padding: 20px;
  max-width: 1400px;
  margin: 0 auto;
}

.main-game-area {
  display: flex;
  flex-direction: column;
  gap: 30px;
  flex: 1;
  margin: 20px 0;
}

.score-section,
.game-section {
  width: 100%;
}

/* ========== LAYOUT PARA TELAS GRANDES ========== */
@media (min-width: 1024px) {
  .main-game-area {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    gap: 80px;
    margin: 40px 70px;
  }

  .score-section {
    width: 35%;
    order: 1;
    padding: 50px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .game-section {
    width: 70%;
    order: 2;
  }

  .game-section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}

/* ========== LAYOUT PARA TELAS MÉDIAS ========== */
@media (min-width: 768px) and (max-width: 1023px) {
  .main-game-area {
    gap: 40px;
  }

  .app-container {
    padding: 15px;
  }
}

/* ========== LAYOUT PARA MOBILE ========== */
@media (max-width: 767px) {
  .app-container {
    gap: 5px;
    padding: 10px;
    text-align: center;
  }

  .main-game-area {
    gap: 20px;
    margin: 15px 0;
  }
}
</style>