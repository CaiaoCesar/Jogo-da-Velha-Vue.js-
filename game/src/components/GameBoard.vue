<template>
    <h2>Player 1 vs Player 2</h2>
    <div class="board">   
      <div class="cell" v-for="n in 9" :key="n">{{ n }}</div>
    </div>
</template>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
.board {
  display: grid;
  grid-template-columns: repeat(3, 3em);
  grid-gap: 0.5em;
  margin: 2rem auto;
  width: fit-content;
}

.cell{
  border: 1px solid #42b983;
  cursor: pointer;
  font-size: 2em;
  display: flex;
  justify-content: center;
  align-items: center;
}
.cell:hover{
  background-color: #42b983;
  transition: 0.5s;
  Transform: scale(1.1);
}
</style>
