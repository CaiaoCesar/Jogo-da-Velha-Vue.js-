<template>
    <div class="images-container">
        <img alt="Jogo da Velha Logo" src="../assets/logoGame.png">
        <img alt="Jogo da Velha Logo" src="../assets/logoGame3.png">
        <img alt="Jogo da Velha Logo" src="../assets/logoGame2.png">
    </div>
</template>

<script>
export default {
  name: 'ImagesGame'
}
</script>

<style scoped>
.images-container {
  display: flex;
  justify-content: center;
  flex-wrap: nowrap;
  align-items: center;
  gap: 10%;
}
img {
  width: 20%;
  object-fit: contain;
}
</style>