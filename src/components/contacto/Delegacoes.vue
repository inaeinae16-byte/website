<template>
  <section class="section-delegacoes">
    <!-- Cabeçalho -->
    <div class="cabesalho-delegacoes">
      <Svg name="icondelegacoes" style="width: 40px;" />
      <h2>Delegações Províncias</h2>
    </div>

    <div class="container-tabela">
      <!-- Tabela -->
      <table class="tabela-delegacoes">

        <!-- Cabeçalho da tabela -->
        <thead>
          <tr>
            <th>Província</th>
            <th>Endereço</th>
            <th>Telefone</th>
            <th>E-mail</th>
          </tr>
        </thead>

        <!-- Corpo da tabela -->
        <transition-group name="fade-linha" tag="tbody">
          <tr
            v-for="(delegacao, index) in delegacoes"
            :key="index"
          >
            <td>{{ delegacao.provincia }}</td>
            <td>{{ delegacao.endereco }}</td>
            <td>{{ delegacao.telefone }}</td>
            <td>{{ delegacao.email }}</td>
          </tr>
        </transition-group>

      </table>
    </div>

  </section>
</template>


<style scoped>

.section-delegacoes {
  width: 100%;
  max-width: 1180px;
  margin: 70px auto;
  font-family: Semibold;
}

/* Cabeçalho */
.cabesalho-delegacoes {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  margin-bottom: 35px;
}

.cabesalho-delegacoes h2 {
  font-size: var(--f6);
  font-family: bold;
 color: var(--cor-preto);
}

/* Container da tabela */
.container-tabela {
  background: var(--cor-branco);
  border-radius: 10px;
  overflow-x: auto;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.08);
}

/* Tabela */
.tabela-delegacoes {
  width: 100%;
  border-collapse: collapse;
  min-width: 1000px; 
}

/* Cabeçalho */
.tabela-delegacoes thead {
  background: var(--cor-cinza);
}

.tabela-delegacoes th {
  padding: 30px 70px;
  font-size: var(--f3);
  font-family: semibold;
  color: var(--cor-preto);
  text-align: cenetr;
  border-right: 1px solid #dcdcdc;
  border-bottom: 1px solid #dcdcdc;
}

/* Remove borda direita do último th */
.tabela-delegacoes th:last-child {
  border-right: none;
}

/* Corpo */
.tabela-delegacoes td {
  padding: 18px;
  font-size: var(--f3);
  font-family: Regular;
  color: var(--cor-preto);
  vertical-align: top;
  border-right: 1px solid #e1e1e1; 
  border-bottom: 1px solid #e1e1e1;
}

/* Remove borda direita da última coluna */
.tabela-delegacoes td:last-child {
  border-right: none;
}

/* Última linha sem borda inferior */
.tabela-delegacoes tbody tr:last-child td {
  border-bottom: none;
}

/* Animação leve profissional */
.fade-linha-enter-active {
  transition: all 0.35s ease;
}

.fade-linha-enter-from {
  opacity: 0;
  transform: translateY(6px);
}



</style>

<script setup>
import Svg from '../../assets/Svg/Svgs.vue'
// Lista das delegações provinciais
const delegacoes = [
  {
    provincia: 'Cabo Delgado',
    endereco:
      'Av. Eduardo Mondlane, Edifício da Direcção Provincial da Indústria e Comércio, Cidade de Pemba',
    telefone: '+258 84 722 9285',
    email: 'inae.cabodelgado@inae.gov.mz'
  },
  {
    provincia: 'Niassa',
    endereco: 'Av. Filipe Samuel Magaia, Cidade de Lichinga',
    telefone: '+258 86 658 1225',
    email: 'inae.niassa@inae.gov.mz'
  },
  {
    provincia: 'Nampula',
    endereco:
      'Av. 25 de Setembro, edifício da indústria e comércio, 1º andar esquerdo, Cidade de Nampula',
    telefone: '+258 84 758 9444',
    email: 'inae.nampula@inae.gov.mz'
  },
  {
    provincia: 'Zambézia',
    endereco:
      'Av. Marginal, edifício dos Serviços Provinciais de Economia e Finanças, 1º piso, Cidade de Quelimane',
    telefone: '+258 84 840 0540',
    email: 'inaezambezia@inae.gov.mz'
  },
  {
    provincia: 'Tete',
    endereco: 'Avenida da Independência, Cidade de Tete',
    telefone: '+258 87 722 6624',
    email: 'inae.tete@inae.gov.mz'
  },
  {
    provincia: 'Manica',
    endereco: 'Rua Cidade de Lichinga nº 311, Cidade de Chimoio',
    telefone: '+258 86 819 7607 / 84 819 7428',
    email: 'inae.manica@inae.gov.mz'
  },
   {
    provincia: 'Sofala',
    endereco: 'Rua Francismo Gorjão nº 370, Ponta Gea, Cidade da Beira',
    telefone: '+258 82 441 1836 ',
    email: 'inae.sofala@inae.gov.mz'
  },
   {
    provincia: 'Inhambane',
    endereco: 'Av. Acordos de Lusaka, ao lado da Gráfica Sul Save, Cidade de Inhambane',
    telefone: '+258 86 672 8240 ',
    email: 'inae.inhamban@inae.gov.mz'
  },
   {
    provincia: 'Gaza',
    endereco: 'Av. Samora Machel, EN1 Cidade de Xai-Xai.',
    telefone: '+258 84 609 9000 |86 609 9000  ',
    email: 'inae.gaza@inae.gov.mz'
  },
   {
    provincia: 'Provincia de Maputo',
    endereco: 'Rua 11.135, em frente ao Centro Cultural do Banco de Moçambique, Cidade da Matola.',
    telefone: '+258 87 327 3463',
    email: 'inae.provinciademaputo@inae.gov.mz'
  },
   {
    provincia: 'Cidade Maputo',
    endereco: 'Av. Josina Machel n⁰ 151, Cidade de Maputo.',
    telefone: '+258 87 327 3463',
    email: 'inae.cidadedemaputogaza@inae.gov.mz'
  },

]
</script>