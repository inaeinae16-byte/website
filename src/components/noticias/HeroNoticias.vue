<template>
  <div class="noticias-container" :style="{ backgroundImage: `url(${banner})` }">
    <!--Overlay de deixar escuro a imagem com opacity-->
    <div class="overlay"></div>

    <!--Conteudo principal-->
    <div class="noticias">
        <h1 class="noticias-title">Notícias Recentes</h1>
        <p class="noticias-subtitulo">Fique por dentro das últimas notícias</p>

        <!--Barra de pesquisa-->
        <div class="pesquisa-container">
            <Svg name="lupaNoticias" />
            <input type="text" placeholder="Buscar Notícias" class="pesquisa-input">
        </div>
    </div>

   </div>
  
</template>

<style scoped>

.noticias-container {
  position: relative;
  width: 100%;
  height: 400px;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

/* opacidade sobre a imagem de fundo */
.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.65); 
  z-index: 1;
}

.noticias {
  position: relative;
  z-index: 2;
  text-align: center;
  color: var(--cor-branco);
  max-width: 800px;
  width: 100%;
  padding: 0 20px;
}

.noticias-title {
  font-size: 4rem;
  font-family: semibold;
  margin: 0 0 12px 0;
  letter-spacing: 0.5px;
  color: var(--cor-branco);
}


.noticias-subtitulo {
  font-size: var(--f3);
  font-family: semibold;
  margin: 0 0 40px 0;
  color: var(--cor-branco);
  letter-spacing: 0.3px;
}

.pesquisa-container {
  position: relative;
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  align-items: center;
}

.pesquisa-container svg {
  position: absolute;
  left: 20px;
  width: 20px;
  height: 20px;
  pointer-events: none;
  z-index: 1;
}


.pesquisa-input {
  width: 100%;
  padding: 20px 10px 20px 52px;
  font-size: var(--f3);
  font-family: regular;
  border: none;
  border-radius: 8px;
  background-color: rgba(255, 255, 255, 0.15); /* Efeito vidro fosco */
  backdrop-filter: blur(10px);/* Deixar a opaco */
  color: var(--cor-branco);
  outline: none;
  transition: all 0.3s ease;
}

.pesquisa-input::placeholder {
  color: rgba(255, 255, 255, 0.6);
  font-family: regular;
}

/* Estado focus do input */
.pesquisa-input:focus {
  background-color: rgba(255, 255, 255, 0.2);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

/* Responsividade para tablets */
@media (max-width: 768px) {
  .noticias-container {
    height: 350px;
  }
  
  .noticias-title {
    font-size: 2.2rem;
  }
  
  .noticias-subtitulo {
    font-size: 0.9rem;
    margin-bottom: 30px;
  }
  
  .pesquisa-input {
    padding: 14px 18px 14px 48px;
    font-size: 0.9rem;
  }
  
  .pesquisa-container svg {
    left: 16px;
  }
}

/* Responsividade para mobile */
@media (max-width: 480px) {
  .noticias-container {
    height: 300px;
  }
  
  .noticias-title {
    font-size: 1.8rem;
  }
  
  .noticias-subtitulo {
    font-size: 0.85rem;
  }
}
</style>

<script setup>
import Svg from '../../assets/Svg/Svgs.vue'

// Fundo do banner (usa URL resolvida para trabalhar com Vite)
const banner = new URL('@/assets/banner01.png', import.meta.url).href
</script>