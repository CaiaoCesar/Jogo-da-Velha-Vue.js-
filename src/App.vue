<template>
  <div class="app-container">
    <HeaderInfo></HeaderInfo>
    <ImagesGame></ImagesGame>

    <div class="main-game-area">
      <div class="score-section">
        <ScoreTable ref="scoreTable" @player-names-updated="handlePlayerNamesUpdate">
          <template #reset-button>
            <div class="btn-reset-desktop">
              <button @click="handleResetButtonClick">Zerar Estatísticas</button>
            </div>
          </template>
        </ScoreTable>
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
    },

    handleResetButtonClick() {
      this.$refs.gameBoard.resetGame();
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
  display: flex; 
  justify-content: center; 
}

.app-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  padding: 20px;
  max-width: 1400px;
  width: 100%; 
  align-items: center;
}

.main-game-area {
  display: flex;
  flex-direction: column;
  gap: 30px;
  flex: 1;
  margin: 20px 0;
  width: 100%; 
  align-items: center; 
}

.game-section {
  width: 100%;
  display: flex;
  justify-content: center; 
  align-items: center; /* ← Adicionar se não existir */
  flex-direction: column; /* ← Para alinhar verticalmente */
}

.score-section {
  width: 100%;
  display: flex;
  justify-content: center; 
}

.btn-reset-desktop {
  display: none; 
}

.my-swal-popup {
  font-family: "Montserrat", sans-serif !important;
}

.my-swal-title {
  font-family: "Montserrat", sans-serif !important;
  font-weight: 700 !important;
}

.my-swal-button {
  font-family: "Montserrat", sans-serif !important;
  font-weight: 600 !important;
}

.my-swal-cancel-button {
  font-family: "Montserrat", sans-serif !important;
  font-weight: 600 !important;
}

/* ========== LAYOUT PARA MOBILE ========== */
@media (max-width: 767px) {
  .app-container {
    gap: 5px;
    padding: 10px;
    text-align: center;
    align-items: center; 
  }

  .main-game-area {
    gap: 20px;
    margin: 15px 0;
    width: 100%;
    align-items: center;
  }

  /* GARANTE QUE AS SEÇÕES VOLTEM A 100% NO MOBILE */
  .score-section,
  .game-section {
    width: 100% !important;
    max-width: 100% !important;
    padding: 0 !important;
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

  .score-section,
  .game-section {
    width: 100%;
  }
}

/* ========== LAYOUT PARA TELAS GRANDES ========== */
@media (min-width: 1024px) {
  .main-game-area {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    gap: 80px;
    margin: 40px 0; 
    width: 100%;
    max-width: 1200px; 
    justify-content: center; 
  }

  .score-section {
    width: 400px; 
    order: 1;
    padding: 32px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .game-section {
    width: 600px; 
    order: 2;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .btn-reset-desktop {
    display: flex;
    width: 280px;
    height: 70px;
    border-radius: 20px;
    overflow: hidden;
    border: 3px solid #42b983;
    cursor: pointer;
    justify-content: center;
    align-items: center;
  }

  .btn-reset-desktop button {
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-style: normal;
    font-size: 1.3em;
    width: 100%;
    height: 100%;
    color: wheat;
    background-color: transparent;
    border: none;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .btn-reset-desktop:hover {
    color: #121413c8;
    background-color: #42b983;
    border: 3px solid #e0e8e4c8;
    Transform: scale(1.025);
  }

  .btn-reset-desktop:hover button {
    color: #121413c8;
    background-color: #42b983;
  }
}
</style>