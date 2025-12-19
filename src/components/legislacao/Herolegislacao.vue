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
          <Svg :key="secaoAtiva" :name="secaoAtual.icone"  class="icone-secao"/>
        </transition>

        <h2 class="titulo-secao">{{ secaoAtiva }}</h2>
      </div>

      <!--  LADO DIREITO (DOCUMENTOS)  -->
      <div class="lado-direito">
        
        <!-- anima SOMENTE os documentos -->
        <transition-group name="lista-slide" tag="ul" class="lista-documentos"  >
            <li v-for="(doc, index) in secaoAtual.documentos" :key="index" class="item-documento" >
            <a :href="doc.pdf" target="_blank" rel="noopener" class="link-documento">
              <span class="icone-pdf">
                    <Svg name="iconpdf" style="width: 30px;" />
              </span>

                {{ doc.titulo }}
            </a>
          </li>

        </transition-group>
      </div>
          </div>
        </section>
</template>


<style scoped>

.container-geral {
  max-width: 1200px;
  margin:30px auto;
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
  border-radius:0px 0px 20px 20px ;
  overflow: hidden;
}


.lado-esquerdo {
  background: var(--cor-branco);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 40px 20px;
  border: 2px solid #28782e;
  border-radius:0px 0px 0px 20px ;
}

.icone-secao {
  width: 100px;
  margin-bottom: 15px;
}

.titulo-secao {
  font-size: var(--f5);
  font-family: semibold;
  color: var(--cor-verde);
}

/* LADO DIREITO */
.lado-direito {
  padding: 120px;
  background: #edf3ef;
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
  transition: all 0.59s ease;
}

.lista-slide-enter-from {
  opacity: 0;
  transform: translateY(5px);
}

.link-documento {
  display: flex;
  align-items: center;
  gap: 10px;
  text-decoration: none;
  color: #3b8253;
  font-size: var(--f3);
  font-family: semibold;
  width: 100%;
  transition: all .4s;
}

.link-documento:hover {
  margin-left: 10px;
}

/* =========================
   RESPONSIVIDADE
========================= */

/* TABLET */
@media (max-width: 1024px) {
  .conteudo {
    grid-template-columns: 1fr 1.5fr;
  }

  .lado-direito {
    padding: 60px;
  }

  .icone-secao {
    width: 80px;
  }

  .aba {
    padding: 18px 40px;
  }
}

/* MOBILE */
@media (max-width: 768px) {

  /* Abas com scroll horizontal */
  .abas {
    overflow-x: auto;
    white-space: nowrap;
    padding-bottom: 5px;
  }

  .aba {
    flex: 0 0 auto;
    padding: 15px 30px;
    font-size: var(--f2);
  }

  /* Conteúdo em coluna */
  .conteudo {
    grid-template-columns: 1fr;
    border-radius: 0px 0px 20px 20px;
  }

  .lado-esquerdo {
    border-radius: 0;
    border-bottom: 2px solid #28782e;
  }

  .icone-secao {
    width: 70px;
  }

  .titulo-secao {
    font-size: var(--f4);
  }

  .lado-direito {
    padding: 30px 20px;
  }

  .item-documento {
    padding: 8px 0;
  }

  .link-documento {
    font-size: var(--f2);
  }
}

/* MOBILE PEQUENO */
@media (max-width: 480px) {
  .icone-secao {
    width: 60px;
  }

  .lado-direito {
    padding: 20px 15px;
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
    icone: "iconcarinho-comercio",
    documentos: [
      {
         titulo:
         "Regulamento obrigatoriedade da afixação dos preços",
          pdf: new URL(
            "https://drive.google.com/file/d/1kBPDsPpTzQHsOenle1nPZfIP3xConyUY/view?usp=sharing"
          ).href,
        
        },
      {
         titulo:
         "Regulamento fixação de margens de lucro para produtos básicos",
          
        
        },
      {
         titulo:
         "Regulamento Licenciamento da Actividade Comercial",
          pdf: new URL(
            "https://drive.google.com/file/d/1cTQYcR7WQ6hX947o8SRquEgwVbsxh9Nj/view?usp=sharing"
          ).href,
        
        },
  
    ],
  },
  Turismo: {
    icone: "turismo",
    documentos: [
          {
         titulo:
                "Regulamento de agências e profissionais de turismo",
          pdf: new URL(
            "https://drive.google.com/file/d/17pkrXYCjK05CKu3tkUgTNBG-YWp6r8of/view?usp=sharing"
          ).href,
        
        },
          {
         titulo:
                "Regulamento de animação turistica",
          pdf: new URL(
            "https://drive.google.com/file/d/19UtM6Vd1okMDGk406pSdxnZno1Su4Cxj/view?usp=sharing"
          ).href,
        
        },
          {
         titulo:
                "Regulamento de turismo, restauração e dança",
          pdf: new URL(
            "https://drive.google.com/file/d/1lV80SwrKBlqbvtEJcyJR93KOdcaZ6_uF/view?usp=sharing"
          ).href,
        
        },
          {
         titulo:
                "Regulamento do direito de habitação periódica",
          pdf: new URL(
            "https://drive.google.com/file/d/1r_tyrLogZFRxwzckunkZ2mFz2eU-S63o/view?usp=sharing"
          ).href,
        
        },
          {
         titulo:
                "Regulamento do transporte turistico",
          pdf: new URL(
            "https://drive.google.com/file/d/1Ci71wDoyafxXUnoNJbLQNt6LDD7NtoxH/view?usp=sharing"
          ).href,
        
        },
    ],
  },
  Desporto: {
    icone: "desporto",
    documentos: [
    {
         titulo:
                "Licenciamento de Actividade Desportivas",
          pdf: new URL(
            "https://drive.google.com/file/d/1QhhhhuuEZegClEh1ZkQ0NJJ5dTR3fBJu/view?usp=sharing"
          ).href,
        
        },
    ],
  },
  Educação: {
    icone: "educação",
    documentos: [
      {
         titulo:
                "Regulamento dos centros infantis",
          pdf: new URL(
            "https://drive.google.com/file/d/1SwVZffWpSlLoQEXwDIz4iLb9ouP016kd/view?usp=sharing"
          ).href,
        
        },
      {
         titulo:
                "Regulamento de inpeções as instituições de ensino superior",
          pdf: new URL(
            "https://drive.google.com/file/d/1HNHk1rgawqHnRvMBM7EvFLenYRzCK3gq/view?usp=sharing"
          ).href,
        
        },
      {
         titulo:
                "Regulamento de Licenciamento de instituições de ensino profissional",
          pdf: new URL(
            "https://drive.google.com/file/d/1Bywn6MsVnDFa6qurMsf47itDVWw4TDy7/view?usp=sharing"
          ).href,
        
        },
          {
         titulo:
                "Regulamento da Educação particular",
          pdf: new URL(
            "https://drive.google.com/file/d/1PDzkxCNrJ-kcXOR_2OpClPD6BUSum_cs/view?usp=sharing"
          ).href,
        
        },
    ],
  },
  Cultura: {
    icone: "cultura",
    documentos: [
       {
         titulo:
                "Lei do Audio-visual e do cinema",
          pdf: new URL(
            "https://drive.google.com/file/d/1hQuoCngilwux4EohJjsjVT4DH9HRcDOp/view?usp=sharing"
          ).href,
        
        },

        //2
         {
         titulo:
                "Lei dos direitos de autor e direitos conexos",
          pdf: new URL(
            "https://drive.google.com/file/d/1Z7Q-R0mfmjGxra7Ig_qxEq1_Su6yUzeF/view?usp=sharing"
          ).href,
        
        },

        //3
         {
         titulo:
                "Lei que regula e diciplina o acesso de menores tanto a recintos públicos",
          pdf: new URL(
            "https://drive.google.com/file/d/1WmVOOWAcAV4CiTzcIyCwNr2owKVb7rxh/view?usp=sharing"
          ).href,
        
        },

        //4
         {
         titulo:
                "Regulamento de espetaculos e divertimentos públicos",
          pdf: new URL(
            "https://drive.google.com/file/d/1bcRxVKjPrBvsqCv3sQZ1ECssSc-cMP5P/view?usp=sharing"
          ).href,
        
        },

        //5
         {
         titulo:
                "Regulamento sobre menores, diversão noturna e álcool.",
          pdf: new URL(
            "https://drive.google.com/file/d/1DsRZvih1BDU0NgOmAK73rCqyMphEEiMT/view?usp=sharing"
          ).href,
        
        },

        //6
         {
         titulo:
                "Regulamento da lei de jogos de fortuna ou azar",
          pdf: new URL(
            "https://drive.google.com/file/d/194tYcwCNeLGAfc8pnQJbjX1eijDiWQhJ/view?usp=sharing"
          ).href,
        
        },
    ],
  },
  Transversal: {
    icone: "transversal",
    documentos: [
     {
         titulo:
                "Código de propriedade industrial",
          pdf: new URL(
            "https://drive.google.com/file/d/1kSagcBH832KdKs8nk2OJ9EOUHXgVNmvu/view?usp=sharing"
          ).href,
        
        },
        //2
        {
         titulo:
                "Código de publicidade de decreto",
          pdf: new URL(
            "https://drive.google.com/file/d/1GUK6_cly9YjwgJ3xMJzDPFA0PK_7AM-0/view?usp=sharing"
          ).href,
        
        },

        //3
        {
         titulo:
                "Lei de defesa do consumidaor",
          pdf: new URL(
            "https://drive.google.com/file/d/1vTJCrPr44EvwYv-hfoPboU8YAQzmKXqp/view?usp=sharing"
          ).href,
        
        },

        //4
        {
         titulo:
                "Regulamento do consumo e comercialização de tabaco",
          pdf: new URL(
            "https://drive.google.com/file/d/1cy_2MD2Pd3BcoHDPUOuixfy3xXoIuOys/view?usp=sharing"
          ).href,
        
        },

        //5
        {
         titulo:
                "Regulamento de fortificação de alimentos",
          pdf: new URL(
            "https://drive.google.com/file/d/1XEGif3JKH9C50ZFkqwo4cTcZ3QwtEAld/view?usp=sharing"
          ).href,
        
        },

        //6
        {
         titulo:
                "Regulamento sobre a gestão e controlo do saco plástico",
          pdf: new URL(
              "https://drive.google.com/file/d/1cWxv80MN5wTbogPJbP82rz6dqyL4oMKP/view?usp=sharing"
          ).href,
        
        },

        //7
        {
         titulo:
                "Regulamento sobre controlo de bebidas alcoólicas",
          pdf: new URL(
            "https://drive.google.com/file/d/1j4qdUPdVNzwIQgU6-pitiiTe1km1KZJ5/view?usp=sharing"
          ).href,
        
        },

        //8
        {
         titulo:
                "Regime simplificado para licenciar atividades económicas",
          pdf: new URL(
            "https://drive.google.com/file/d/1DnOX2AFNjhV19tHB97lPWTrYSsYoxETs/view?usp=sharing"
          ).href,
        
        },
    ],
  },
};

/* SECÇÃO ATUAL */
const secaoAtual = computed(() => conteudos[secaoAtiva.value]);
</script>

