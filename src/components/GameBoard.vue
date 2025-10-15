<template>
  <div class="game-info">
    <p>Rodada: <strong>{{ round }}</strong></p>
    <p><strong>{{ getPlayerName(playerStart) }} iniciou o jogo!</strong></p>
    <p>Vez do Jogador: <strong>{{ getPlayerName(currentPlayer) }}</strong></p>

    <!-- Mensagem de resultado do jogo -->
    <div v-if="gameMessage" class="game-message" :class="messageType">
      {{ gameMessage }}
    </div>
  </div>

  <div class="board">
    <div class="cell" v-for="(cell, index) in cells" :key="index" @click="cellClick(index)">
      <img v-if="cell === 'O'" src="../assets/O.png" alt="Imagem O" />
      <img class="X" v-else-if="cell === 'X'" src="../assets/X.png" alt="Imagem X" />
    </div>
  </div>

  <div class="btn-restart">
    <button @click="restartGame">Reiniciar</button>
  </div>
</template>

<script>
export default {
  props: {
    playerNames: {
      type: Object,
      default: () => ({
        playerX: "Jogador 1",
        playerO: "Jogador 2"
      })
    }
  },
  data() {
    return {
      cells: Array(9).fill(""),
      currentPlayer: "X",
      playerStart: "X",
      round: 1,
      gameFinished: false,
      gameMessage: "",
      messageType: ""
    };
  },
  methods: {
    cellClick(index) {
      if (this.cells[index] !== "" || this.gameFinished) return;

      this.cells[index] = this.currentPlayer;

      const gameOver = this.checkStateGame();

      if (!gameOver) {
        this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
      }
    },

    restartGame() {
      this.cells = Array(9).fill("");
      this.round++;
      this.gameFinished = false;
      this.gameMessage = "";
      this.messageType = "";

      this.playerStart = this.playerStart === "X" ? "O" : "X";
      this.currentPlayer = this.playerStart;
    },

    checkStateGame() {
      const winConditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6],
      ];

      for (const condition of winConditions) {
        const [a, b, c] = condition;

        if (
          this.cells[a] &&
          this.cells[a] === this.cells[b] &&
          this.cells[a] === this.cells[c]
        ) {
          const winner = this.cells[a];
          const winnerName = this.getPlayerName(winner);

          this.gameFinished = true;
          this.gameMessage = `🎉 ${winnerName} ganhou! 🎉`;
          this.messageType = "win";

          this.$emit('game-ended', { winner: winner, type: 'win' });

          return true;
        }
      }

      if (this.cells.every((cell) => cell !== "")) {
        this.gameFinished = true;
        this.gameMessage = "🤝 Empatou! Deu velha! 🤝";
        this.messageType = "draw";

        this.$emit('game-ended', { winner: null, type: 'draw' });

        return true;
      }

      return false;
    },

    getPlayerName(playerSymbol) {
      if (playerSymbol === 'X') {
        return this.playerNames.playerX;
      } else if (playerSymbol === 'O') {
        return this.playerNames.playerO;
      }
      return playerSymbol;
    }
  }
};
</script>

<style scoped>
.game-info {
  font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
  font-weight: 700;
  font-style: normal;
  font-size: 1.1em;
  padding: 10px;
  text-align: center;
  min-height: 120px;
}

.game-info strong {
  color: #42b983;
}

.game-message {
  margin-top: 15px;
  padding: 12px 20px;
  border-radius: 10px;
  font-weight: 900;
  font-size: 1.2em;
  animation: fadeIn 0.5s ease-in;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.game-message.win {
  background: linear-gradient(135deg, #42b983, #26dda9);
  color: white;
  border: 3px solid #2a945b;
}

.game-message.draw {
  background: linear-gradient(135deg, #ffb347, #ffcc33);
  color: #333;
  border: 3px solid #e6a336;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.board {
  display: grid;
  grid-template-columns: repeat(3, 7.5em);
  grid-template-rows: repeat(3, 7.5em);
  grid-gap: 0px;
  margin: 2rem auto;
  width: fit-content;
}

.cell {
  border: 3px solid #42b983;
  cursor: pointer;
  font-size: 2em;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.cell:hover {
  background-color: #75ad94c8;
  transition: 0.5s;
  Transform: scale(1.025);
}

.cell img {
  width: 80%;
  height: auto;
}

.cell img.X {
  width: 65%;
  height: auto;
}

.btn-restart {
  display: flex;
  width: 40%;
  height: 50px;
  margin: auto;
  margin-bottom: 20px;
  border-radius: 20px;
  overflow: hidden;
  border: 3px solid #42b983;
  cursor: pointer;
}

.btn-restart button {
  font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
  font-weight: 900;
  font-style: normal;
  font-size: 1.5em;
  width: 100%;
  height: 100%;
  color: wheat;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.btn-restart:hover {
  color: #121413c8;
  background-color: #42b983;
  border: 3px solid #e0e8e4c8;
  Transform: scale(1.025);
}

.btn-restart:hover button {
  color: #121413c8;
  background-color: #42b983;
}

@media (max-width: 600px) {
    .game-info {     
        font-size: 1em;
        margin: auto;
        padding: 0px;
    }

    .board{
      margin-top: 0px;
    }
  }
</style>
