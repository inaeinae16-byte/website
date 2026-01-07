<template>
  <div class="hero-banner">
    <div class="hero-overlay"></div>
    <img :src="banner" alt="Banner" class="hero-image"/>
    
    <div class="hero-content">
      <div class="hero-text">
        <h1 class="hero-title">
          A Inspeção Nacional das Atividades Económicas (INAE) é o órgão do Estado responsável por fiscalizar e promover o <br>
          cumprimento das normas que regulam a produção e a comercialização de bens e serviços em Moçambique. 
        </h1>
      </div>
   
    </div>
  </div>
</template>

<script setup>
import banner from '@/assets/image 29.png'
</script>

<style scoped>
.hero-banner {
  position: relative;
  width: 100%;
  height: 400px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.hero-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.3) 0%,
    rgba(0, 0, 0, 0.5) 50%,
    rgba(0, 0, 0, 0.7) 100%
  );
  z-index: 1;
}

.hero-content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 40px;
  z-index: 2;
}

.hero-text {
  flex: 1;
  display: flex;
  align-items: center;
}

.hero-title {
  color: white;
  font-size: var(--f4);
 font-family: bold;
  line-height: 1.6;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  padding: 50px;
}

.hero-footer {
  display: flex;
  align-items: center;
  gap: 15px;
  background: rgba(255, 255, 255, 0.95);
  padding: 20px 25px;
  border-radius: 8px;
  backdrop-filter: blur(10px);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}


/* Responsivo */
@media (max-width: 768px) {
  .hero-banner {
    height: 500px;
  }
  
  .hero-content {
    padding: 24px;
  }
  
  .hero-title {
    font-size: 1.1rem;
  }
  
  .hero-footer {
    flex-direction: column;
    text-align: center;
    padding: 16px;
  }
  
  .footer-text {
    font-size: 0.85rem;
  }
}

@media (max-width: 480px) {
  .hero-banner {
    height: 450px;
  }
  
  .hero-content {
    padding: 16px;
  }
  
  .hero-title {
    font-size: 1rem;
  }
}
</style>