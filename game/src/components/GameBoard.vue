<template>
  <h2>Que vença o melhor!</h2>
  <div class="board">
    <div class="cell" v-for="(cell, index) in cells" :key="index" @click="cellClick(index)">
      <img v-if="cell === 'O'" src="../assets/O.png" alt="Imagem O" />
      <img v-else-if="cell === 'X'" src="../assets/X.png" alt="Imagem X" />
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
    };
  },
  methods: {
    cellClick(index) {
      if (this.cells[index] !== "") return;

      this.cells[index] = this.currentPlayer;

      this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
    },

    restartGame() {
      this.cells = Array(9).fill("");
    },
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
  width: 70%;
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
