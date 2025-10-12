<template>
    <div class="input-names">
        <input class="input-p1" v-model="playerOne" type="text" placeholder="Nome do Jogador 1">
        <input class="input-p2" v-model="playerTwo" type="text" placeholder="Nome do Jogador 2">
    </div>
    <h3>Placar:</h3>
    <div class="tables-container">
        <table>
            <tr>
                <th>{{ playerOne || "Jogador 1" }} (X):</th>
                <td>{{ scoreX }}</td>
            </tr>
        </table>
        <table>
            <tr>
                <th>{{ playerTwo || "Jogador 2" }} (O):</th>
                <td>{{ scoreO }}</td>
            </tr>
        </table>
    </div>
    <div class="draws">
        <p>Empates: {{ scoreDraw }}</p>
    </div>
</template>

<script>
export default {
  name: 'ScoreTable',
  data() {
      return {
          playerOne: "",
          playerTwo: "",
          scoreX: 0,
          scoreO: 0,
          scoreDraw: 0
      }
  },
  methods: {
    updateScore(result) {
      if (result.type === 'win') {
        if (result.winner === 'X') {
          this.scoreX++;
        } else if (result.winner === 'O') {
          this.scoreO++;
        }
      } else if (result.type === 'draw') {
        this.scoreDraw++;
      }
    },
    
    resetScore() {
      this.scoreX = 0;
      this.scoreO = 0;
      this.scoreDraw = 0;
    }
  }
}
</script>


<style scoped>
h3{
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-style: normal;
    font-size: 2.2em
}
.tables-container{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 1%;
    width: 100%;
    border: #26dda9 solid 2px;
}
table {  
    text-align: center;
    width: 30%;
    height: 10%;
}
th, td{
    background-image: linear-gradient(90deg, #26dda9, #a0f7e0);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    padding: 2px;
    font-size: 1.5em;
}
.input-name{
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-bottom: 10px;
}
input{
    padding: 5px;
    border-radius: 5px;
    border: 2px solid #42b983;
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-style: normal;
    font-size: 1.1em;    
}
.draws{
    background-image: linear-gradient(90deg, #26dda9, #a0f7e0);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    padding: 2px;
    font-size: 2em;
}
</style>