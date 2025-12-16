<template>
  <section class="container-geral">
    <!-- Buttons-->
    <nav class="abas">
      <button v-for="secao in secoes" :key="secao" class="aba" :class="{ ativa: secaoAtiva === secao }" @click="secaoAtiva = secao" >
        {{ secao }}
      </button>
    </nav>

    <!-- Conteudo  -->
    <div class="conteudo">
      <!--LADO ESQUERDO (ÍCONE + TÍTULO) -->
      <div class="lado-esquerdo">
        <!-- anima SOMENTE no ícone -->
        <transition name="icone-fade" mode="out-in">
          <Svg :key="secaoAtiva" :src="secaoAtual.icone" class="icone-secao" alt="Ícone da secção" />
        </transition>

        <h2 class="titulo-secao">{{ secaoAtiva }}</h2>
      </div>

      <!--  LADO DIREITO (DOCUMENTOS)  -->
      <div class="lado-direito">
        
        <!-- anima SOMENTE os documentos -->
        <transition-group name="lista-slide" tag="ul" class="lista-documentos"  >
             <li v-for="(doc, index) in secaoAtual.documentos" :key="doc + index" class="item-documento" >
            <span class="icone-pdf"><Svg name="iconpdf" style="width: 30px;" /></span>
            {{ doc }}
          </li>
        </transition-group>
      </div>
    </div>
  </section>
</template>


<style scoped>

.container-geral {
  max-width: 1200px;
  margin:100px auto;
}

/* ABAS */
.abas {
  display: flex;
  gap: 8px;
  margin-bottom: 10px;
  justify-content: start;
}

.aba {
  padding: 25px 63px;
  border: none;
  border-radius: 10px 10px 0px 0px;
  background: #e6e6e6;
  cursor: pointer;
  font-family: semibold;
  font-size: var(--f3);
  transition: all 0.25s ease;
}

.aba:hover {
  background: var(--cor-branco);
}

.aba.ativa {
  background: var(--cor-verde);
  color: var(--cor-branco);
}

/* CONTEÚDO */
.conteudo {
  display: grid;
  grid-template-columns: 1fr 2fr;
  background: var(--cor-cinza);
  border-radius:0px 0px  10px 10px ;
  overflow: hidden;
}

/* LADO ESQUERDO */
.lado-esquerdo {
  background: var(--cor-verde);
  border-right: 1px solid #d8e4dc;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 40px 20px;
}

.icone-secao {
  width: 60px;
  margin-bottom: 15px;
}

.titulo-secao {
  font-size: var(--f4);
  font-family: semibold;
}

/* LADO DIREITO */
.lado-direito {
  padding: 120px;
}

.lista-documentos {
  list-style: none;
  padding: 0;
  margin: 0;
}

.item-documento {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 0;
  font-family: Regular;
  font-size: var(--f3);
}

/* ANIMAÇÃO DO ÍCONE */
.icone-fade-enter-active,
.icone-fade-leave-active {
  transition: all 0.35s ease;
}

.icone-fade-enter-from {
  opacity: 0;
  transform: scale(0.9);
}

.icone-fade-leave-to {
  opacity: 0;
  transform: scale(1.05);
}

/* ANIMAÇÃO DA LISTA */
.lista-slide-enter-active {
  transition: all 0.35s ease;
}

.lista-slide-enter-from {
  opacity: 0;
  transform: translateY(8px);
}

/* RESPONSIVO */
@media (max-width: 768px) {
  .conteudo {
    grid-template-columns: 1fr;
  }

  .lado-esquerdo {
    border-right: none;
    border-bottom: 1px solid #d8e4dc;
  }
}


</style>

<script setup>
import { ref, computed } from "vue";

import Svg from '../../assets/Svg/Svgs.vue'

/* SECÇÃO ATIVA */
const secaoAtiva = ref("Comércio");

/* LISTA DE SECÇÕES */
const secoes = [
  "Comércio",
  "Turismo",
  "Desporto",
  "Educação",
  "Cultura",
  "Transversal",
];

/* CONTEÚDOS */
const conteudos = {
  Comércio: {
    icone: "",
    documentos: [
      "Regulamento obrigatoriedade da afixação dos preços",
      "Normas gerais do comércio",
      "Fiscalização e sanções",
    ],
  },
  Turismo: {
    icone: "/icons/turismo.svg",
    documentos: [
      "Licenciamento de empreendimentos turísticos",
      "Classificação hoteleira",
    ],
  },
  Desporto: {
    icone: "/icons/desporto.svg",
    documentos: [
      "Regulamento de eventos desportivos",
      "Normas de segurança",
    ],
  },
  Educação: {
    icone: "/icons/educacao.svg",
    documentos: [
      "Regulamento de instituições privadas",
    ],
  },
  Cultura: {
    icone: "/icons/cultura.svg",
    documentos: [
      "Proteção do património cultural",
    ],
  },
  Transversal: {
    icone: "/icons/transversal.svg",
    documentos: [
      "Normas gerais aplicáveis",
    ],
  },
};

/* SECÇÃO ATUAL */
const secaoAtual = computed(() => conteudos[secaoAtiva.value]);
</script>

