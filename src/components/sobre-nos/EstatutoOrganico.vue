<template>
  <section class="section">
    <div class="cabesalho">
     <Svg name="Estrutura" style="width: 40px;"/>
      <h2>Estrutura Orgânica Central da INAE</h2>
    </div>

    
      <p class="paragrafo-cabesalho">
        De acordo com o Estatuto Orgânico aprovado pela Resolução nº 2/2018, de 28 de Fevereiro,
         a nível central a INAE possui a seguinte estrutura orgânica:
      </p>

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

    <div class="button-0rgonogrma">
        <a href="https://inae.gov.mz/assets/images/diversos/ORGANOGRAMA%20INAE%202023.pdf" class="btn-ver">Ver Orgonograma</a>
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

.paragrafo-cabesalho {
  font-size: var(--f3);
  color: var(--cor-preto);
  margin-top: 50px;
  margin-bottom: 70px;
  text-align: center;
  font-family: semibold;
 
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

.button-0rgonogrma {
  margin-top: 50px;
  display: flex;
  justify-content: center;
  background: var(--cor-verde);
  width: 100%;
  padding: 30px 0px 30px 0px;
  border-radius: 20px;
  margin: 0 auto;
  max-width: 400px;
  margin-top: 30px;
  cursor: pointer;
  transition: 1.3s ease;
}

.button-0rgonogrma:hover {
  background: #469560;
  scale: 1.05;
}

.btn-ver {
    color: var(--cor-branco);
    text-decoration: none;
    font-size: var(--f9);
    text-align: center;

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

.button-0rgonogrma{
  width: 100%;
  max-width: 300px;
  padding: 20px 0px 20px 0px;
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
    pergunta: 'Direcção',
    resposta:
      'As competências do Inspector-Geral consistem em dirigir as actividades da INAE, representar a INAE no plano interno e externo, coordenar e supervisionar as suas actividades, apreciar recursos hierárquicos das decisões proferidas pelos Delegados da INAE, submeter à aprovação do Ministro da tutela sectorial o Regulamento Interno da INAE, bem como os assuntos que sejam da sua competência, os planos de actividade e orçamento, o plano estratégico e o relatório anual de actividades, e submeter anualmente a conta de gerência às autoridades competentes. Compete-lhe igualmente propor ao Ministro da tutela sectorial a nomeação de Directores e Delegados da INAE, nomear Chefes de Departamento Central autónomos e não autónomos e Chefes de Repartição, gerir os meios humanos, materiais e financeiros da INAE, avaliar e homologar a avaliação de desempenho dos Funcionários e Agentes do Estado afectos à INAE, assinar os contratos necessários à prossecução das suas actividades, negociar a contratação de pessoal técnico, assessores e consultores, e exercer as demais competências conferidas por lei ou que lhe forem delegadas. Por sua vez, o Inspector-Geral Adjunto tem como competências coadjuvar o Inspector-Geral no desempenho das suas funções, substituí-lo nas suas ausências e impedimentos, e exercer os poderes e desempenhar outras tarefas que lhe forem delegados.'
  },
  {
    pergunta:
      'Direcção de Operações de Pesquisa e Inteligencia Economica (DOPIE)',
    resposta:
      'A Direcção de Operações de Pesquisa e Inteligência Económica tem como função definir e implementar estratégias de investigação e inteligência da INAE, seleccionando investigadores, formando equipas e controlando os resultados das suas actividades. Compete-lhe investigar e conduzir operações a nível nacional e internacional, especialmente na defesa dos direitos de propriedade industrial, direitos de autor, publicidade e outras matérias que possam representar perigo à saúde pública e ao ambiente. Esta direcção assegura também a gestão do plano de investigação e inteligência, estabelece parcerias com instituições nacionais e internacionais, articula com entidades competentes para garantir informação actualizada sobre direitos de propriedade intelectual e assegura o tratamento, acesso e difusão de informação científica, técnica e jurídica relevante. Além disso, colabora com organismos nacionais e internacionais na repressão de ilícitos contra a propriedade industrial, promove estudos para melhorar a fiscalização das actividades económicas e coopera com entidades que contribuam para o desenvolvimento da competitividade empresarial em Moçambique. A Direcção é dirigida por um Director de Operações, nomeado pelo Ministro que superintende a área da Indústria e Comércio, sob proposta do Inspector-Geral da INAE.'
  },
  {
    pergunta:
      'Direcção de Operações de Indústria, Comercio, Turismo e Transporte (DOICTT)',
    resposta:
      'A Direcção de Operações da Indústria, Comércio, Turismo e Transporte tem como função ordenar e realizar inspecções às unidades económicas nas áreas da sua especialização, bem como supervisionar a implementação de estratégias, planos e programas de inspecção e fiscalização. Compete-lhe apresentar relatórios periódicos das actividades, participar na elaboração de estudos e legislação do sector e propor a revogação ou anulação de actos que não estejam em conformidade com a legislação vigente. Esta direcção é também responsável por verificar o cumprimento das normas de segurança, higiene e preservação ambiental, investigar denúncias, queixas e reclamações, e propor medidas correctivas. Além disso, promove acções de educação e sensibilização dos agentes económicos e do público, recolhe e trata informações operacionais, submete amostras de produtos suspeitos para análise e presta pareceres técnicos quando solicitados. No âmbito da fiscalização, controla a comercialização de produtos mineiros, o uso de gás e instalações eléctricas, fiscaliza o transporte de mercadorias e produtos alimentares, o funcionamento de oficinas e outras actividades relacionadas com transporte e prestação de serviços, assegurando o cumprimento da legislação em todo o território nacional. A Direcção é dirigida por um Director de Operações, nomeado pelo Ministro da tutela sectorial, sob proposta do Inspector-Geral da INAE.'
  },
  {
    pergunta:
      'Direcção de Operações da Educação, Cultura e Desportos (DOECD)',
    resposta:
      'A Direcção de Operações da Educação, Cultura e Desporto tem como função garantir a coordenação e operacionalização das actividades nas áreas da sua especialização, bem como ordenar e realizar inspecções às unidades económicas desses sectores. Compete-lhe supervisionar a implementação de estratégias, planos e programas de inspecção e fiscalização, apresentar relatórios periódicos das actividades e participar na elaboração de estudos e legislação do sector. Esta direcção é responsável por fiscalizar livrarias, gráficas, recintos de diversão, estabelecimentos de produção e realização de espectáculos, bem como locais de produção e comercialização de materiais desportivos e publicitários. Além disso, assegura o cumprimento da legislação sobre direitos de autor e direitos conexos, fiscaliza a circulação e comercialização de obras de arte, artesanato e música, verifica o cumprimento das normas de segurança, higiene e preservação ambiental, investiga denúncias e reclamações e propõe medidas correctivas. Compete-lhe ainda prestar pareceres técnicos e realizar outras tarefas que lhe forem superiormente definidas. A Direcção é dirigida por um Director Nacional, nomeado pelo Ministro da tutela sectorial, sob proposta do Inspector-Geral da INAE.'
  },
  {
    pergunta:
      'Gabite jurídico e Contencioso (GJC)',
    resposta:
      'O Gabinete Jurídico e Contencioso tem como função emitir pareceres jurídicos sobre os assuntos relacionados com as actividades da INAE e assegurar a assistência jurídica a todas as suas unidades orgânicas. Compete-lhe manter actualizada a base de dados de legislação e outros diplomas relevantes, preparar projectos de actos normativos em coordenação com outros órgãos e participar em negociações para o estabelecimento de acordos e instrumentos jurídicos. Este gabinete garante também a interpretação e aplicação uniforme da legislação inspectiva, investiga denúncias, queixas e reclamações e propõe medidas correctivas. Além disso, presta assessoria jurídica à Direcção da INAE, contribui para o acesso e organização da informação jurídica, acompanha e controla processos judiciais de contencioso, colabora com entidades nacionais e internacionais na repressão de ilícitos no comércio e assegura o apoio técnico-jurídico necessário ao funcionamento da instituição. Compete-lhe ainda elaborar relatórios periódicos das suas actividades e realizar outras tarefas que lhe forem superiormente atribuídas.'
  },
  {
    pergunta:
      'Departamento de Planificação e Cooperacação (DPC)',
    resposta:
      'O Departamento de Planificação e Cooperação tem como função coordenar o processo de planificação da INAE, elaborando, em conjunto com as demais unidades orgânicas, a proposta do plano de actividades, orçamento e respectivos relatórios, de acordo com as metodologias em vigor. Compete-lhe recolher, tratar, centralizar e sistematizar a informação de planificação e estatística das actividades inspectivas, bem como garantir a sua organização e circulação dentro da instituição. Este departamento é também responsável por preparar e organizar sessões dos Conselhos Consultivos, reuniões de Direcção e outros eventos institucionais. Além disso, propõe e acompanha acordos de cooperação com entidades nacionais e estrangeiras, monitoriza a implementação de programas, projectos e acções de cooperação e mantém as unidades orgânicas informadas sobre o seu desenvolvimento. Compete-lhe ainda realizar outras tarefas que lhe forem superiormente atribuídas. O Departamento é dirigido por um Chefe de Departamento Central Autónomo, nomeado pelo Inspector-Geral da INAE.'
  },
    {
    pergunta:
      'Departamento de Planificação e Cooperacação (DAF-FFF)',
    resposta:
      'O Departamento de Planificação e Cooperação tem como função coordenar o processo de planificação da INAE, elaborando, com a participação das demais unidades orgânicas, o plano de actividades, o orçamento e os respectivos relatórios, de acordo com as metodologias em vigor. Compete-lhe recolher, tratar, centralizar e organizar a informação de planificação e os dados estatísticos das actividades inspectivas, garantindo a sua circulação dentro da instituição. É também responsável por preparar e organizar sessões dos Conselhos Consultivos, reuniões de Direcção e outros eventos institucionais, bem como propor, acompanhar e avaliar acordos de cooperação com entidades nacionais e estrangeiras relacionadas com a inspecção das actividades económicas. Além disso, coordena e monitoriza programas, projectos e acções de cooperação e realiza outras tarefas que lhe forem superiormente atribuídas. O Departamento é dirigido por um Chefe de Departamento Central Autónomo, nomeado pelo Inspector-Geral da INAE.'
  },
    {
    pergunta:
      'Departamento de Recursos Humanos (DRH)',
    resposta:
      'O Departamento dos Recursos Humanos tem como função planificar, coordenar e gerir os recursos humanos da INAE, assegurando a elaboração, gestão e actualização do quadro do pessoal, bem como a aplicação das normas de selecção, contratação, progressão e promoção. Compete-lhe propor e implementar planos de formação académica e profissional, organizar e manter actualizado o sistema de informação de pessoal, e garantir a aplicação do Estatuto Geral dos Funcionários e Agentes do Estado e demais legislação aplicável. Este departamento é também responsável por planificar e implementar políticas de gestão de recursos humanos, coordenar acções relacionadas com saúde, HIV e SIDA, doenças crónicas, género e inclusão da pessoa com deficiência, e assegurar a avaliação de desempenho dos funcionários, incluindo a implementação do sistema de gestão de desempenho na Administração Pública. Além disso, gere o sistema de remunerações e benefícios, produz estatísticas internas e mantém actualizada a base de dados do pessoal, bem como assegura a implementação das normas de previdência social. O Departamento é dirigido por um Chefe de Departamento Central Autónomo, nomeado pelo Inspector-Geral da INAE.'
  },
    {
    pergunta:
      'Departamento de Comunicação, Imagem e Relações Públicas (DCIRP)',
    resposta:
      'O Departamento de Comunicação, Imagem e Relações Públicas tem como função promover e difundir a imagem da INAE, bem como divulgar informações sobre as actividades de fiscalização e inspecção das actividades económicas. Compete-lhe servir de elo entre a INAE e os órgãos de comunicação social, assegurando os contactos institucionais e contribuindo para o esclarecimento da opinião pública através da divulgação de informação oficial. Este departamento é responsável por produzir e divulgar o Boletim Informativo e outros materiais de comunicação, planificar e desenvolver estratégias integradas de comunicação e imagem, organizar e manter actualizado o ficheiro de notícias relacionadas com as actividades da instituição e garantir o cumprimento dos aspectos protocolares. Compete-lhe ainda realizar outras tarefas que lhe forem superiormente atribuídas. O Departamento é dirigido por um Chefe de Departamento Central Autónomo, nomeado pelo Inspector-Geral da INAE.'
  },
    {
    pergunta:
      'Departamento de Aquisições (DA)',
    resposta:
      'A Direcção de Administração e Finanças tem como função elaborar propostas de orçamento de funcionamento e investimento, escriturar os livros de registo e assegurar a prestação de contas. Compete-lhe gerir o sistema de recepção, circulação e expedição da correspondência, garantir a segurança, manutenção e correcta utilização das instalações da instituição, prestar apoio técnico e logístico às diferentes unidades orgânicas, administrar os bens patrimoniais conforme as normas vigentes e assegurar a sua preservação e protecção. Este departamento implementa o Sistema Nacional de Arquivos do Estado, administra e gere os arquivos e a documentação da instituição, elabora relatórios de execução do plano e orçamento, bem como a Conta de Gerência a submeter ao Tribunal Administrativo, zelando pelo cumprimento das normas de administração e gestão dos recursos financeiros e patrimoniais. Compete-lhe ainda coordenar a execução e controlo do orçamento, articular com as unidades orgânicas para análise conjunta de planos e orçamento, gerir actividades de economato, aprovisionamento e transporte, garantir a correcta utilização de materiais, equipamentos e instalações, manter actualizado o cadastro dos bens patrimoniais e assegurar a gestão eficiente dos recursos financeiros. A Direcção é dirigida por um Chefe de Departamento Central Autónomo, nomeado pelo Inspector-Geral da'
  },
    {
    pergunta:
      'Departamento de Tecnologias e Sistemas de informação (DTSI)',
    resposta:
      'O Departamento de Tecnologia e Sistemas de Informação tem como função conceber e propor políticas e estratégias para as tecnologias de informação e comunicação da INAE, visando melhorar a qualidade dos serviços, aumentar a eficiência e racionalizar custos. Compete-lhe definir padrões de hardware e software a adquirir, promover o desenvolvimento e modernização das tecnologias de comunicação e informação, elaborar planos para introdução de novas tecnologias e implementar e monitorar o Plano Estratégico de TIC da instituição. Este departamento adota uma estratégia de governação das TIC, definindo normas para a seleção, aquisição e utilização de infraestruturas e sistemas de informação, concebe, implementa e gere sistemas integrados de informação, garantindo recolha, tratamento e disponibilização segura e eficiente de dados, articulando com os utilizadores sobre o acesso à informação. Além disso, promove a racionalização de recursos, processos e infraestruturas tecnológicas, assegura a instalação, funcionamento e gestão do ciclo de vida dos equipamentos informáticos, presta assistência aos funcionários para melhor utilização dos sistemas, propõe formação em TIC e representa a INAE junto de entidades interministeriais e internacionais na área das tecnologias de informação e comunicação. O Departamento é dirigido por um Chefe de Departamento Central Autónomo, nomeado pelo Inspector-Geral da INAE.'
  },
]

// Função para abrir e fechar perguntas
function alternarPergunta(index) {
  perguntaAtiva.value =
    perguntaAtiva.value === index ? null : index
}
</script>
