<template>
  <h2>Que vença o melhor!</h2>
  <div class="game-info">
    <p>Rodada: <strong>{{ round }}</strong></p> 
    <p><strong>{{ playerStart }} iniciou o jogo!</strong></p>
    <p>Vez do Jogador: <strong>{{ currentPlayer }}</strong></p>
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
  data() {
    return {
      cells: Array(9).fill(""),
      currentPlayer: "X",
      playerStart: "X",
      round: 1,
      gameFinished: false // Nova variável para controlar se o jogo acabou
    };
  },
  methods: {
    cellClick(index) {
      // Se célula já preenchida ou jogo acabou, não faz nada
      if (this.cells[index] !== "" || this.gameFinished) return;

      this.cells[index] = this.currentPlayer;

      // Verifica se o jogo terminou
      const gameOver = this.checkStateGame();

      if (!gameOver) {
        this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
      }
    },

    restartGame() {
      this.cells = Array(9).fill("");
      this.round++;
      this.gameFinished = false; // Reseta o estado do jogo

      this.playerStart = this.playerStart === "X" ? "O" : "X";
      this.currentPlayer = this.playerStart;
    },

    checkStateGame() {
      const winConditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6],
      ];

      // Verifica vitória
      for (const condition of winConditions) {
        const [a, b, c] = condition;

        if (
          this.cells[a] &&
          this.cells[a] === this.cells[b] &&
          this.cells[a] === this.cells[c]
        ) {
          const winner = this.cells[a];
          
          this.gameFinished = true; // Marca que o jogo acabou
          
          // EMIT: Envia o vencedor para o componente pai
          this.$emit('game-ended', { winner: winner, type: 'win' });
          
          setTimeout(() => {
            alert(`O jogador ${winner} ganhou!`);
          }, 10);
          
          return true;
        }
      }

      // Verifica empate
      if (this.cells.every((cell) => cell !== "")) {
        this.gameFinished = true; // Marca que o jogo acabou
        
        // EMIT: Envia empate para o componente pai
        this.$emit('game-ended', { winner: null, type: 'draw' });
        
        setTimeout(() => {
          alert("Empatou ou melhor dizendo 'Deu velha!'");
        }, 10);
        
        return true;
      }
      
      return false;
    }
  },
};
</script>

<style scoped>
h2 {
  font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
  font-weight: 900;
  font-size: 1.8em;
  font-style: normal;
}
.game-info {
  font-family: "Montserrat", sans-serif;
  font-optical-sizing: auto;
  font-weight: 700;
  font-style: normal;
  font-size: 1.1em;
  padding: 10px;
  text-align: center;
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
  width: 20%;
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
</style>
