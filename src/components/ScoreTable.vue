<template>
     <h2>Que vença o melhor!</h2>
    <div class="input-names">
        <input id="player-one" name="player-one" class="input-p1" v-model="playerOne" type="text"
            placeholder="Nome do Jogador 1" @input="updatePlayerNames">
        <input id="player-two" name="player-two" class="input-p2" v-model="playerTwo" type="text"
            placeholder="Nome do Jogador 2" @input="updatePlayerNames">
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
        },
        
        updatePlayerNames() {
            // Emite os nomes dos jogadores para o componente pai
            this.$emit('player-names-updated', {
                playerX: this.playerOne || "Jogador 1",
                playerO: this.playerTwo || "Jogador 2"
            });
        }
    },
    mounted() {
        // Emite os nomes iniciais quando o componente é carregado
        this.updatePlayerNames();
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
h3 {
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-style: normal;
    font-size: 2.2em
}

.tables-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 30px;
    width: 100%;
    margin-bottom: 20px;
}

table {
    text-align: center;
    width: 300px;
    border-collapse: collapse; 
}

tr {
    display: flex;
    justify-content: space-between; /* Nome à esquerda, placar à direita */
    align-items: center;
    width: 100%;
    padding: 10px 15px;
    background: rgba(38, 221, 169, 0.1);
    border-radius: 12px;
    border: 2px solid #26dda9;
}

th,
td {
    background-image: linear-gradient(90deg, #26dda9, #a0f7e0);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-size: 1.5em;
    white-space: nowrap; 
}

th {
    text-align: left;
    flex: 1; /* Ocupa o espaço disponível */
}

td {
    text-align: right;
    min-width: 40px; /* Largura mínima para o número */
    font-size: 1.8em;
    font-weight: 900;
}


input {
    padding: 5px;
    border-radius: 5px;
    border: 2px solid #42b983;
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-style: normal;
    font-size: 1.1em;
}

.draws {
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


@media (max-width: 600px) {
    h3 {
        font-size: 1.8em;
    }

    .tables-container {
        flex-direction: column;
        gap: 15px;
    }

    table {
        width: 90%;
        max-width: 300px;
    }

    tr {
        padding: 8px 12px;
    }

    th, td {
        font-size: 1.3em;
    }

    td {
        font-size: 1.6em;
    }

    .input-names {
        flex-direction: column;
        align-items: center;
        gap: 10px;
    }

    .input-p1, .input-p2 {
        width: 90%;
        max-width: 300px;
    }

    .draws {
        font-size: 1.3em;
    }
}
</style>