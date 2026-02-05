<template> 
  <div class="container">
    <h1 class="title">NATUREZA E ATRIBUIÇÃO</h1>
    
    <div class="content">
      <div class="section">
        <div class="icon-wrapper">
        <Svg name="iconnatureza" class="icon" />
        </div>
        <h2 class="section-title">NATUREZA</h2>
        <p class="section-text">
          A Inspecção Nacional das Actividades Económicas,
         abreviadamente designada por INAE, é uma instituição pública,
          dotada de personalidade jurídica e autonomia administrativa. </p>
      </div>

      <div class="section">
        <div class="icon-wrapper">
          <Svg name="iconatribuicoes" class="icon" />
        </div>
        <h2 class="section-title">ATRIBUIÇÕES</h2>
        <p class="section-text">
          A INAE tem como atribuição a fiscalização do cumprimento da legislação reguladora do exercício das actividades económicas e a
           defesa do consumidor.
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>

.container {
  background-color: var(--cor-branca);
  padding: 60px 40px;
  min-height: 60vh;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.title {
  color: var(--cor-verde);
  font-size: var(--f5);
  font-family: bold;
  margin-bottom: 60px;
}

.content {
  display: flex;
  gap: 280px;
  max-width: 1200px;
  width: 100%;
  justify-content: center;
}

.section {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: start;
  border: 5px solid var(--cor-verde);
  border-radius: 60px;
  padding: 20px 40px;
}

.icon-wrapper {
  width: 90px;
  margin-bottom: 20px;
  position: relative;
}

.icon {
  width: 100%;
  animation: iconFloat 4s ease-in-out infinite;
}

@keyframes iconFloat {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.section:nth-child(1) .icon {
  animation-delay: 0s;
}

.section:nth-child(2) .icon {
  animation-delay: 1.5s;
}

.section-title {
  color: var(--cor-verde);
  font-size: var(--f4);
  font-family: bold;
  text-align: center;
  margin-bottom: 20px;
}

.section-text {
  color: var(--cor-preta);
  font-size: var(--f3);
  font-family: semibold;
  text-align: start;
  line-height: 1.5;
  letter-spacing: 0.1px;
}

@media (max-width: 768px) {
  .content {
    flex-direction: column;
    gap: 50px;
  }
  
  .title {
    font-size: 24px;
  }
}
</style>

<script setup>
  import Svg from  '../../assets/Svg/Svgs.vue'
</script>