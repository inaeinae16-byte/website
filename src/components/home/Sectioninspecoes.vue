<template>
<div class="container" ref="statsContainer">
  <div class="card">
    <div class="icon">
      <Svg name="lupa" class="lupa" />
    </div>
    <div class="Numero">+{{ formatNumber(currentInspections) }}</div>
    <div class="Descricao">INSPEÇÕES MENSAIS</div>
  </div>

    <div class="card">
    <div class="icon">
      <Svg name="estabelicimentos" class="lupa2" />
    </div>
    <div class="Numero">+ {{ formatNumber(currentEstablishments) }}</div>
    <div class="Descricao">ESTABELICIMENTOS FISCALIZADOS</div>
  </div>
</div>
</template>

<style scoped>
.container {
  display: flex;
  flex-wrap: nowrap;
  justify-content: center;
  gap: 110px;
  padding: 20px;
}

.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  min-width: 280px;
  max-width: 540px;
  height: 350px;
  background-color: var(--cor-branca);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.20);
  border-radius: 20px;
padding: 45px 58px;
  transition: transform 0.30s ease;

}

.card:hover {
  transform: translateY(-15px);
 box-shadow: 0px 9px 28px -4px rgba(59, 130, 83, 1);
}

.lupa, .lupa2{
  width: 90px;
}

.icon {
  width: 80px;
  height: 80px;
  margin-bottom: 60px;
}

.Numero {
  font-size: var(--f7);
  font-family: bold;
  margin-bottom:  10px;

}

.Descricao {
  font-family: semibold;
  font-size: var(--f4); 
}

@media (max-width: 500px) {

  .container {
    flex-direction: column;        
    gap: 40px;                     
    padding: 10px;
  }

  .card {
    min-width: 100%;  
    max-width: 100%;            
    height: auto;                  
    padding: 40px 20px;
  }

  .icon,
  .lupa,
  .lupa2 {
    width: 70px;                  
    height: auto;
    margin-bottom: 0px;
  }

  .Numero {
    font-size: var(--f6);
  }

  .Descricao {
    font-size: calc(var(--f4) - 7px);
  }
}




</style>

<script setup>
// Importa as funções necessárias do Vue para o setup
import { ref, onMounted, onBeforeUnmount } from 'vue'
import Svg from '../../assets/Svg/Svgs.vue'

// Referência ao elemento do container (para observar quando fica visível)
const statsContainer = ref(null)
// Armazena o valor atual da contagem de inspeções mensais
const currentInspections = ref(0)
// Armazena o valor atual da contagem de estabelecimentos fiscalizados
const currentEstablishments = ref(0)
// Define o valor alvo para inspeções mensais (onde a contagem vai parar)
const targetInspections = 500
// Define o valor alvo para estabelecimentos (onde a contagem vai parar)
const targetEstablishments = 300000
// Flag para garantir que a animação só aconteça uma vez
const hasAnimated = ref(false)
// Variável para armazenar a instância do IntersectionObserver
let observer = null

// Função que configura o observador de interseção
// Detecta quando o elemento entra na área visível da tela
const setupIntersectionObserver = () => {
  // Opções do observador
  const options = {
    threshold: 0.4,      // Dispara quando 50% do elemento está visível
  }

  // Cria o observador
  observer = new IntersectionObserver((entries) => {
    // Para cada elemento observado
    entries.forEach(entry => {
      // Se o elemento está visível na tela E ainda não foi animado
      if (entry.isIntersecting && !hasAnimated.value) {
        // Marca como já animado (para não repetir)
        hasAnimated.value = true
        // Inicia a animação dos números
        animateNumbers()
      }
    })
  }, options)

  // Começa a observar o elemento do container
  observer.observe(statsContainer.value)
}

// Função que anima os números de 0 até o valor alvo
const animateNumbers = () => {
  // Duração total da animação em milissegundos (4 segundos)
  const duration = 4000
  // Número de passos (frames) que a animação terá
  const steps = 60
  // Intervalo entre cada passo em milissegundos (divide duração total pelos passos)
  const intervalTime = duration / steps

  // Calcula quanto incrementar por passo para as inspeções
  const inspectionIncrement = targetInspections / steps
  // Calcula quanto incrementar por passo para os estabelecimentos
  const establishmentIncrement = targetEstablishments / steps

  // Contador que rastreia em qual passo da animação estamos
  let currentStep = 0

  // Inicia um intervalo que executa a cada intervalTime ms
  const interval = setInterval(() => {
    // Incrementa o contador de passos
    currentStep++

    // Se ainda não atingimos o total de passos
    if (currentStep <= steps) {
      // Atualiza o valor de inspeções (incrementando gradualmente)
      // Math.round arredonda o valor, Math.min garante que não ultrapasse o alvo
      currentInspections.value = Math.min(
        Math.round(inspectionIncrement * currentStep),
        targetInspections
      )
      // Atualiza o valor de estabelecimentos (da mesma forma)
      currentEstablishments.value = Math.min(
        Math.round(establishmentIncrement * currentStep),
        targetEstablishments
      )
    } else {
      // Se já completou todos os passos, define os valores finais exatos
      currentInspections.value = targetInspections
      currentEstablishments.value = targetEstablishments
      // Para o intervalo (limpa o timer)
      clearInterval(interval)
    }
  }, intervalTime)
}

// Função que formata um número com separador de milhares
const formatNumber = (num) => {
  // Usa toLocaleString para formatar de acordo com a região pt-BR (Brasil)
  return num.toLocaleString('pt-BR')
}

// Hook do Vue que executa quando o componente é montado na tela
onMounted(() => {
  // Configura o observador quando o componente carrega
  setupIntersectionObserver()
})

// Hook do Vue que executa antes do componente ser removido da tela
onBeforeUnmount(() => {
  // Se o observador existe, desconecta-o para evitar vazamento de memória
  if (observer) {
    observer.disconnect()
  }
})
</script>