<template>
    <h3>Placar:</h3>
    <div class="tables-container">
        <table>
            <tr>
                <th>Jogador 1:</th>
                <td>0</td>
            </tr>
        </table>
        <table>
            <tr>
                <th>Jogador 2:</th>
                <td>0</td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
  
}
</script>

<style scoped>
h3{
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 900;
    font-style: normal;
    font-size: 1.5em
}
.tables-container{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 5%;
    width: 100%;
}
table {
    background-color: #615b5bff;
    color: #fff;
    text-align: center;
    width: 35%;
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
    font-size: 2em;
}
</style>