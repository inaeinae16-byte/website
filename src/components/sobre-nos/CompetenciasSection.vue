<template>
  <div class="hero-banner">
    <div class="hero-overlay"></div>
    <img :src="banner" alt="Banner" class="hero-image"/>
    
    <div class="hero-content">
      <div class="hero-text">
        <h1 class="hero-title">
         A Inspeção Nacional das Atividades Económicas (INAE) é o órgão do Estado responsável por fiscalizar e promover o cumprimento das normas que regulam a produção e a comercialização de bens e serviços em Moçambique. 
        </h1>
      </div>
   
    </div>
  </div>
</template>

<script setup>
import banner from '@/assets/background inae.png'
</script>

<style scoped>
.hero-banner {
  position: relative;
  width: 100%;
  height: calc(100% - 90px);
  overflow: hidden;
}

.hero-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  background-repeat: no-repeat;
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
  justify-content: center;
}

.hero-title {
    color: white;
    font-size: var(--f4);
    font-family: 'Regular';
    line-height: 1.7;
    padding: 0px 350px 0 350px;
    text-align: center;
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

  
  .hero-content {
    padding: 50px;
  }
  
  .hero-title {
    font-size: 1.2rem;
    line-height: 1.5;
    padding: 0px 50px 0 50px;
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