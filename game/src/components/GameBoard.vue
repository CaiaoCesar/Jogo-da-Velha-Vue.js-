<template>
  <h2>Que vença o melhor!</h2>
  <div class="board">
    <div class="cell" v-for="(cell, index) in cells" :key="index" @click="cellClick(index)">
      <img v-if="cell === 'O'" src="../assets/O.png" alt="Imagem O" />
      <img v-else-if="cell === 'X'" src="../assets/X.png" alt="Imagem X" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cells: Array(9).fill(""),
      currentPlayer: 'X'
    };
  },
  methods: {
    cellClick(index) {
      if (this.cells[index] !== "") return;

      this.cells[index] = this.currentPlayer;

      this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';


    }
  }
}
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
</style>
