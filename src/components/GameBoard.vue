<template>
  <div class="game-info">
    <p>Rodada: <strong>{{ round }}</strong></p>
    <p><strong>{{ getPlayerName(playerStart) }} iniciou o jogo!</strong></p>
    <p>Vez do Jogador: <strong>{{ getPlayerName(currentPlayer) }}</strong></p>
  </div>

  <div class="board">
    <div class="cell" v-for="(cell, index) in cells" :key="index" @click="cellClick(index)">
      <img v-if="cell === 'O'" src="../assets/O.png" alt="Imagem O" />
      <img class="X" v-else-if="cell === 'X'" src="../assets/X.png" alt="Imagem X" />
    </div>
  </div>

  <div class="btn-restart">
    <button @click="resetGame">Zerar Jogo</button>
  </div>
</template>

<script>
import Swal from 'sweetalert2';

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
      gameFinished: false
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

    // Método antigo - ainda usado pelos alerts
    restartGame() {
      this.cells = Array(9).fill("");
      this.round++;
      this.gameFinished = false;
      this.playerStart = this.playerStart === "X" ? "O" : "X";
      this.currentPlayer = this.playerStart;
    },

    // NOVO MÉTODO - Zera completamente o jogo
    resetGame() {
      Swal.fire({
        title: "🔄 Zerar Jogo?",
        text: "Isso irá resetar a rodada atual e o placar!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonText: 'Sim, zerar tudo!',
        cancelButtonText: 'Cancelar',
        confirmButtonColor: '#42b983',
        cancelButtonColor: '#ff6b6b',
        background: '#2d3748',
        color: '#ffffff',
        width: '400px',
        customClass: {
          popup: 'my-swal-popup',
          title: 'my-swal-title',
          confirmButton: 'my-swal-button',
          cancelButton: 'my-swal-cancel-button'
        }
      }).then((result) => {
        if (result.isConfirmed) {
          // Reseta tudo no GameBoard
          this.cells = Array(9).fill("");
          this.round = 1;
          this.gameFinished = false;
          this.playerStart = "X";
          this.currentPlayer = "X";
          
          // Emite evento para o componente pai resetar o placar também
          this.$emit('reset-game');
          
          Swal.fire({
            title: "✅ Jogo Zerado!",
            text: "Rodada e placar resetados!",
            icon: 'success',
            timer: 2000,
            showConfirmButton: false,
            background: '#2d3748',
            color: '#ffffff',
            customClass: {
              popup: 'my-swal-popup',
              title: 'my-swal-title'
            }
          });
        }
      });
    },

    checkStateGame() {
      const winConditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6],
      ];

      for (const condition of winConditions) {
        const [a, b, c] = condition;

        if (this.cells[a] && this.cells[a] === this.cells[b] && this.cells[a] === this.cells[c]) {
          const winner = this.cells[a];
          const winnerName = this.getPlayerName(winner);

          this.gameFinished = true;
          
          Swal.fire({
            title: `🎉 ${winnerName} venceu! 🎉`,
            icon: 'success',
            confirmButtonText: 'Jogar Novamente',
            confirmButtonColor: '#42b983',
            background: '#2d3748',
            color: '#ffffff',
            width: '400px',
            customClass: {
              popup: 'my-swal-popup',
              title: 'my-swal-title',
              confirmButton: 'my-swal-button'
            },
            timer: 4000,
            timerProgressBar: true
          }).then(() => {
            this.restartGame();
          });

          this.$emit('game-ended', { winner: winner, type: 'win' });
          return true;
        }
      }
    
      if (this.cells.every((cell) => cell !== "")) {
        this.gameFinished = true;

        Swal.fire({
          title: "🤝 Empate! Deu velha! 🤝",
          icon: 'info',
          confirmButtonText: 'Jogar Novamente',
          confirmButtonColor: '#42b983',
          background: '#2d3748',
          color: '#ffffff',
          width: '400px',
          customClass: {
            popup: 'my-swal-popup',
            title: 'my-swal-title',
            confirmButton: 'my-swal-button'
          },
          timer: 4000,
          timerProgressBar: true
        }).then(() => {
          this.restartGame();
        });

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
/* Seus estilos permanecem os mesmos */
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