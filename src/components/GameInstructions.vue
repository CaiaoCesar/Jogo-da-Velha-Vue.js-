<script>
export default {
    name: 'GameInstructions'
}
</script>

<template>
    <div class="instructions">
        <h3>Como Jogar?</h3>
        <p><strong>Forme uma sequência de 3 símbolos iguais para ganhar! A sequência pode ser vertical, horizontal e
                diagonal.</strong></p>
    </div>

    <div class="footer">
        <div class="footer-content">

            <p>Desenvolvido por <a href="https://github.com/caiaocesar" target="_blank">Caio César</a></p>
            <img src="../assets/github.png" alt="Imagem Github">
        </div>
    </div>
</template>

<style scoped>
.instructions {
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 700;
    font-style: normal;
    font-size: 1.1em;
    padding: 10px;
    text-align: center;
    margin-top: 30px;
}

.footer {
    font-family: "Montserrat", sans-serif;
    font-optical-sizing: auto;
    font-weight: 700;
    font-style: normal;
    font-size: 1.1em;
    padding: 10px;
    text-align: center;
    margin-top: 20px;
}

.footer-content {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
}

.footer img {
    width: 20px;
    height: 20px;
}

.footer img:hover {
    transform: scale(1.05);
    text-shadow: 0 0 10px rgba(38, 221, 169, 0.5);
    transition: all 0.3s ease;
}

.footer a {
    background: linear-gradient(90deg, #26dda9, #a0f7e0);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    text-decoration: none;
    font-weight: 900;
    transition: all 0.3s ease;
}

.footer a:hover {
    transform: scale(1.05);
    text-shadow: 0 0 10px rgba(38, 221, 169, 0.5);
}
</style>