<template>
<section class="areas-atuacao">
  <h2 class="titulo">ÁREAS DE ATUAÇÃO</h2>

  <div class="grande-area">
    <div class="cartao-area">
      <div class="icon">
        <Svg name="comercio" class="comercio" />
      </div>
      <p class="nome-area">Comércio</p>
    </div>
    <!--Turismo-->
      <div class="cartao-area">
      <div class="icon">
        <Svg name="turismo" class="turismo" />
      </div>
      <p class="nome-area">Turismo</p>
    </div>
    <!--Educação-->
      <div class="cartao-area">
      <div class="icon">
        <Svg name="educação" class="educacao" />
      </div>
      <p class="nome-area">Educação</p>
    </div>
    <!--Cultura-->
      <div class="cartao-area">
      <div class="icon">
        <Svg name="cultura" class="cultura" />
      </div>
      <p class="nome-area">Cultura</p>
    </div>

    <!--Desporto-->
      <div class="cartao-area">
      <div class="icon">
        <Svg name="desporto" class="desporto" />
      </div>
       <p class="nome-area">Desporto</p>
    </div>

    <!--Transversal-->
      <div class="cartao-area">
      <div class="icon">
        <Svg name="transversal" class="transversal" />
      </div>
      <p class="nome-area">Transversal</p>
    </div>
  </div>
</section>
</template>

<script setup>
import Svg from '../../assets/Svg/Svgs.vue'
</script>

<style scoped>
.areas-atuacao {
  padding: 60px 10px;
  max-width: 1370px;
  margin: 10px auto;
}

.titulo {
  font-size: var(--f5);
  font-family: bold;
  margin-bottom: 40px;
  color: var(--cor-preto);
}

.grande-area {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 23px;
}


.cartao-area {
  position: relative;
  background: var(--cor-fundo); 
  border: 3px solid var(--cor-verde);
  border-radius: 14px;
  padding: 36px 24px 86px;
  box-sizing: border-box;
  transition: transform 0.28s ease, box-shadow 0.28s ease;
  box-shadow: 0 4px 10px rgba(0,0,0,0.05);
  overflow: visible;
}

.cartao-area:hover{
  transform: translateY(-12px);
  box-shadow: 0 10px 30px rgba(0,0,0,0.12);
}


.icon {
  width: 140px;
  height: 120px;
  margin: 0 auto 12px auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.comercio,.turismo,.educacao,.cultura,.desporto,.transversal{
  width: 100%;
  height: 100%;
}

.nome-area {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--cor-fundo);
  text-align: center;
  padding: 16px 0;
  font-size: var(--f4);
  font-family: semibold;
  color: var(--cor-preto);
  border-top: 3px solid var(--cor-verde); 
  border-bottom-left-radius: 12px;
  border-bottom-right-radius: 12px;
}

/* Responsivo colunas diminuem em telas menores*/
@media (max-width: 1200px) {
  .grande-area { grid-template-columns: repeat(3, 1fr); }
}

@media (max-width: 768px) {
  .grande-area { grid-template-columns: repeat(2, 1fr); gap: 18px; }
  .cartao-area { padding: 30px 18px 78px; }
}

@media (max-width: 430px) {
  .grande-area { grid-template-columns: 1fr; }
  .icon { width: 110px; height: 90px; }
}

</style>