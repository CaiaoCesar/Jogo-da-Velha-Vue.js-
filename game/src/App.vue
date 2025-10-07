<template>
  <HeaderInfo></HeaderInfo>
  <img alt="Jogo da Velha Logo" src="./assets/logoGame.png">
  <GameBoard></GameBoard>
  <GameInstructions></GameInstructions>
</template>

<script>
import GameBoard from './components/GameBoard.vue'
import HeaderInfo from './components/HeaderInfo.vue';
import GameInstructions from './components/GameInstructions.vue';

export default {
  name: 'App',
  components: {
    GameBoard,
    HeaderInfo,
    GameInstructions
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2a94a6ff;
  margin-top: 20px;
  background-color: #333;
  padding: 0 20px;
}

img {
  width: 40%;
  max-height: 180px; 
  margin: 10px auto; 
  display: block;
  object-fit: contain;
}
</style>
