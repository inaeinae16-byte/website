<template>
  <section class="section">
    <div class="cabesalho">
     <Svg name="iconcaixademensagem" style="width: 40px;"/>
      <h2>Perguntas Frequentes</h2>
    </div>

    <!-- Lista de perguntas -->
    <div class="lista">

      <!-- Item FAQ -->
      <div v-for="(item, index) in perguntas" :key="index" class="item-faq" >
        <!-- Pergunta -->
        <button class="pergunta-faq" @click="alternarPergunta(index)" >
          
          <span>{{ item.pergunta }}</span>

          <!-- Ícone seta -->
          <span class="seta":class="{ ativa: perguntaAtiva === index }">
            <Svg name="iconperguntasfrequentes"  style="width: 10px;"/>
          </span>
        </button>

        <!-- Resposta -->
        <transition name="fade-slide">
          <div
            v-if="perguntaAtiva === index"
            class="resposta-faq"
          >
            <p>{{ item.resposta }}</p>
          </div>
        </transition>
      </div>

    </div>
  </section>
</template>


<style scoped>
.section {
  width: 100%;
  max-width: 1180px;
  margin: 70px auto;
  font-family: Regular; 
}

.cabesalho {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  margin-bottom: 30px;
}

.cabesalho h2 {
  font-size: var(--f6);
  color: var(--cor-preto);
  font-family: bold;
}

.lista {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Item */
.item-faq {
  background:var(--cor-branco);
  border-radius: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.137);
  overflow: hidden;
}

.pergunta-faq {
  width: 100%;
  background: none;
  border: none;
  padding: 35px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
  font-size: var(--f3);
  font-family: semibold;
  color: var(--cor-preto);
}

/* Ícone seta */
.seta {
  transition: transform 0.3s ease;
}

.seta.ativa {
  transform: rotate(180deg);
}

/* Resposta */
.resposta-faq {
  padding: 0 20px 18px 20px;
  font-size: var(--f3);
  color: #3b3b3b;
  line-height: 1.5;
}

/* Animação */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.5s ease;
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(-10px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

@media (max-width: 768px)  {
 
  .pergunta-faq {
    font-size: var(--f2);
    padding: 25px 15px;
  }

  .resposta-faq {
    font-size: var(--f2);
  }

  .cabesalho h2 {
  font-size: var(--f9);
}
}
</style>

<script setup>
// Importando o icon em SVG
   import Svg from '../../assets/Svg/Svgs.vue'

// Importa ref para reatividade
import { ref } from 'vue'

// Controla qual pergunta está aberta
const perguntaAtiva = ref(null)

// Lista de perguntas e respostas
const perguntas = [
  {
    pergunta: 'A INAE trabalha a noite ?',
    resposta:
      'Sim. Sendo uma entidade que fiscaliza actividades económicas, deve se fazer presente no horário em que os estabelecimentos estão a operar (dia ou noite).'
  },
  {
    pergunta:
      'A poluição sonora é da competência do Conselho Municipal! Qual é o papel da INAE nos locais de diversão noturna e eventos musicais?',
    resposta:
      'O papel da INAE, centra-se na fiscalização do cumprimento da legislação que regula as actividades de diversão noturna e eventos musicais, bem como a defesa do consumidor para garantir a observância dos dispositivos legais e promover as boas práticas no exercício das actividades económicas.'
  },
  {
    pergunta:
      'Porquê é que a INAE, não fiscaliza as igrejas que promovem poluição sonora?',
    resposta:
      'A actividade religiosa não se enquadra na actividade económica, mas sim social, cuja fiscalização é da competência do Ministério da Justiça, Assuntos Constitucionais e Religiosos.'
  },
  {
    pergunta:
      'O que é que a INAE, fiscaliza nos locais de diversão noturna e eventos musicais / show musical?',
    resposta:
      'A INAE fiscaliza os locais de diversão noturna e eventos musicais para garantir o cumprimento da legislação das atividades económicas e a defesa do consumidor. A sua atuação abrange a verificação da legalidade do evento, as condições do local, a segurança dos participantes, a adequação do evento ao público (menores ou maiores de idade) e o controlo da venda e consumo de bebidas alcoólicas e tabaco, especialmente no que diz respeito à proteção de menores.'
  },
  {
    pergunta:
      'É da Competência da INAE Fiscalizar Estabelecimentos de Ensino?',
    resposta:
      'Sim, é da competência da INAE fiscalizar os estabelecimentos de ensino privado, uma vez que estes exercem atividades económicas e não estão excluídos da sua atuação. A INAE atua para assegurar o cumprimento da legislação aplicável e garantir a defesa dos direitos do consumidor, de acordo com a legislação específica em vigor.'
  },
  {
    pergunta:
      'O que é que a INAE fiscaliza nos estabelecimentos de ensino?',
    resposta:
      'A INAE, fiscaliza o cumprimento da legislação, as condições infraestruturais e sempre que necessário a averiguação das reclamações e denúncias.'
  }
]

// Função para abrir e fechar perguntas
function alternarPergunta(index) {
  perguntaAtiva.value =
    perguntaAtiva.value === index ? null : index
}
</script>
