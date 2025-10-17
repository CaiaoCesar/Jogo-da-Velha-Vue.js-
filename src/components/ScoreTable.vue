<template>
    <h2>Jogadores:</h2>
    <div class="input-names">
        <input id="player-one" name="player-one" class="input-p1" v-model="playerOne" type="text"
            placeholder="Nome do Jogador 1" @input="updatePlayerNames">
        <input id="player-two" name="player-two" class="input-p2" v-model="playerTwo" type="text"
            placeholder="Nome do Jogador 2" @input="updatePlayerNames">
    </div>
    <h3>Placar:</h3>
    <div class="main-container">
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

        <div class="reset-button-container">
            <slot name="reset-button"></slot>
        </div>
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
            this.$emit('player-names-updated', {
                playerX: this.playerOne || "Jogador 1",
                playerO: this.playerTwo || "Jogador 2"
            });
        }
    },
    mounted() {
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
    font-size: 2em;
    margin-bottom: 20px;
}

.main-container {
    margin: 0;
    gap: 0;
    padding: 0;
}

.input-names {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-bottom: 20px;
    flex-wrap: wrap;
}

.input-p1,
.input-p2 {
    padding: 10px 15px;
    border-radius: 8px;
    border: 2px solid #42b983;
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-style: normal;
    font-size: 1.1em;
    width: 200px;
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
    justify-content: space-between;
    align-items: center;
    width: 100%;
    padding: 8px 10px;
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
    flex: 1;
}

td {
    text-align: right;
    min-width: 40px;
    font-size: 1.8em;
    font-weight: 900;
}

.draws {
    background-image: linear-gradient(90deg, #26dda9, #a0f7e0);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-size: 1.5em;
    margin-top: 15px;
}

/* ========== RESPONSIVO ========== */
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

    th,
    td {
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

    .input-p1,
    .input-p2 {
        width: 90%;
        max-width: 300px;
    }

    .draws {
        font-size: 1.3em;
    }

    .main-container{
        display: flex; 
        justify-content: center;
    }

    .reset-button-container {
        width: 100%;
        display: flex;
        justify-content: center;
        margin-top: 20px;
    }
}

/* ========== LAYOUT PARA TELAS GRANDES ========== */
@media (min-width: 1024px) {
    .main-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 20px;
    }

    h2 {
        font-size: 2em;
        margin-bottom: 15px;
    }

    h3 {
        font-size: 1.8em;
        margin-bottom: 20px;
    }

    .tables-container {
        flex-direction: column;
        gap: 20px;
        width: 100%;
    }

    table {
        width: 100%;
        max-width: 280px;
    }

    .input-names {
        flex-direction: column;
        gap: 20px;
        margin: 10px 30px;
    }

    .input-p1,
    .input-p2 {
        width: 100%;
        max-width: 280px;
        padding: 12px 25px;
        font-size: 1em;
    }

    .draws {
        font-size: 1.4em;
        margin-top: 7px;
    }

    .reset-button-container {
        margin-top: 25px;
    }
}
</style>