<template>
  <div class="noticia-page">
    <div v-if="noticia" class="noticia-card">
     <!-- CARROSSEL DE IMAGENS -->
      <div class="carousel-container" @mouseenter="pausarAutoplay" @mouseleave="iniciarAutoplay">
        <!-- Imagem Principal -->
        <div class="carousel-main">
          <transition name="fade" mode="out-in">
            <img 
              :key="imagemAtual"
              :src="imagensAtuais[imagemAtual]"
              :alt="`${noticia.titulo} - Imagem ${imagemAtual + 1}`"
              @click="abrirImagem"
              class="carousel-image"
            />
          </transition>

          <!-- Controle Anterior -->
          <button v-if="imagensAtuais.length > 1" class="carousel-btn carousel-prev" @click="imagemAnterior">
            <Svg name="setanoticiaesquerda" />
          </button>

          <!-- Controle Próximo -->
          <button v-if="imagensAtuais.length > 1" class="carousel-btn carousel-next" @click="proximaImagem">
            <Svg name="setanoticia" />
          </button>

          <!-- Indicador de Imagem -->
          <div v-if="imagensAtuais.length > 1" class="carousel-info">
            <span>{{ imagemAtual + 1 }} / {{ imagensAtuais.length }}</span>
          </div>
        </div>

        <!-- Pontos Indicadores -->
        <div v-if="imagensAtuais.length > 1" class="carousel-dots">
          <button
            v-for="(_, index) in imagensAtuais"
            :key="index"
            class="dot"
            :class="{ active: index === imagemAtual }"
            @click="irParaImagem(index)"
          ></button>
        </div>
      </div>

      <!-- MODAL IMAGEM - EXPANDIDA -->
      <transition name="modal-fade">
        <div v-if="imagemAberta" class="imagem-modal" @click.self="fecharImagem">
          <button class="modal-fechar" @click="fecharImagem">✕</button>
          <div class="modal-content">
            <button class="modal-prev" @click="imagemAnteriorModal">❮</button>
            <img :src="imagensAtuais[imagemAtual]" :alt="noticia.titulo" class="imagem-modal-conteudo" />
            <button class="modal-next" @click="proximaImagemModal">❯</button>
          </div>
          <div class="modal-indicator">{{ imagemAtual + 1 }} / {{ imagensAtuais.length }}</div>
        </div>
      </transition>

      <!-- Conteúdo -->
      <div class="card-conteudo">

        <!-- Data -->
        <div class="card-data">
          <Svg name="iconcalendario" />
          <span>Quinta-feira, {{ noticia.data || '28 de Setembro 2025' }}</span>
        </div>

        <!-- Título -->
        <h1 class="card-titulo">{{ noticia.titulo }}</h1>

        <!-- Subtítulo -->
        <p class="card-subtitulo">
          <strong>{{ noticia.subtitulo || 'INAE RECEBE VISITA DO PROCURADOR-GERAL DA REPÚBLICA' }}</strong>
        </p>

        <!-- Texto -->
        <article class="card-texto">
          <p>{{ noticia.fullText || noticia.descricao }}</p>
        </article>

        <!-- Compartilhar -->
        <div class="card-compartilhar">
          <button class="share whatsapp" @click="compartilhar('whatsapp')">
            <Svg name="iconsapp" />
          </button>

          <button class="share facebook" @click="compartilhar('facebook')">
            <Svg name="iconFB" />
          </button>

          <button class="share instagram" @click="compartilhar('instagram')">
            <Svg name="iconIG" />
          </button>

          <button class="share linkedin" @click="compartilhar('linkedin')">
            <Svg name="iconlinkdin" />
          </button>
        </div>

        <!-- Botão oficial -->
        <div class="card-oficial">
          <button class="btn-oficial">
            <Svg name="iconcelo"/>
            Notícia oficial
          </button>
        </div>

      </div>
    </div>

    <!-- Fallback -->
    <div v-else class="sem-dado">
      <p>Notícia não encontrada.</p>
      <button @click="voltar">Voltar</button>
    </div>
  </div>
</template>


<script setup>
import { ref, onMounted, computed, onUnmounted } from 'vue'
import { useRouter } from 'vue-router'
import Svg from '../assets/Svg/Svgs.vue'

const router = useRouter()
const noticia = ref(null)
const imagemAtual = ref(0)
const imagemAberta = ref(false)
const autoplayAtivo = ref(true)
let autoplayInterval = null

// Retorna o array de imagens (com fallback para compatibilidade)
const imagensAtuais = computed(() => {
  if (!noticia.value) return []
  return noticia.value.imagens || (noticia.value.imagem ? [noticia.value.imagem] : [])
})

onMounted(() => {
  try {
    try { console.log('[NoticiaDetalhes] window.history.state:', window.history.state) } catch (e) {}

    noticia.value = window.history.state && window.history.state.noticia ? window.history.state.noticia : null

    if (!noticia.value) {
      try {
        const s = sessionStorage.getItem('noticia_selecionada')
        if (s) noticia.value = JSON.parse(s)
      } catch (e) { noticia.value = noticia.value }
    }
  } catch (e) {
    noticia.value = null
  }

  // Iniciar autoplay
  iniciarAutoplay()
})

onUnmounted(() => {
  pararAutoplay()
})

// FUNÇÕES DE CARROSSEL
const proximaImagem = () => {
  imagemAtual.value = (imagemAtual.value + 1) % imagensAtuais.value.length
  resetarAutoplay()
}

const imagemAnterior = () => {
  imagemAtual.value = (imagemAtual.value - 1 + imagensAtuais.value.length) % imagensAtuais.value.length
  resetarAutoplay()
}

const irParaImagem = (index) => {
  imagemAtual.value = index
  resetarAutoplay()
}

const proximaImagemModal = () => {
  proximaImagem()
}

const imagemAnteriorModal = () => {
  imagemAnterior()
}

// FUNÇÕES DE AUTOPLAY
const iniciarAutoplay = () => {
  if (!autoplayAtivo.value || imagensAtuais.value.length <= 1) return
  
  pararAutoplay()
  autoplayInterval = setInterval(() => {
    imagemAtual.value = (imagemAtual.value + 1) % imagensAtuais.value.length
  }, 5000) // Muda a imagem a cada 5 segundos
}

const pararAutoplay = () => {
  if (autoplayInterval) {
    clearInterval(autoplayInterval)
    autoplayInterval = null
  }
}

const pausarAutoplay = () => {
  pararAutoplay()
}

const resetarAutoplay = () => {
  iniciarAutoplay()
}

// MODAL
const abrirImagem = () => {
  imagemAberta.value = true
  document.body.style.overflow = 'hidden'
  pararAutoplay()
}

const fecharImagem = () => {
  imagemAberta.value = false
  document.body.style.overflow = ''
  iniciarAutoplay()
}

const voltar = () => {
  router.push({ name: 'NoticiasPage' })
}

const compartilhar = (rede) => {
  if (!noticia.value) return
  
  const titulo = encodeURIComponent(noticia.value.titulo)
  const url = encodeURIComponent(window.location.href)
  
  let shareUrl = ''
  
  switch(rede) {
    case 'whatsapp':
      shareUrl = `https://wa.me/?text=${titulo}%20${url}`
      break
    case 'facebook':
      shareUrl = `https://www.facebook.com/sharer/sharer.php?u=${url}`
      break
    case 'instagram':
      navigator.clipboard.writeText(window.location.href)
      alert('Link copiado! Cole no Instagram.')
      return
    case 'linkedin':
      shareUrl = `https://www.linkedin.com/sharing/share-offsite/?url=${url}`
      break
  }
  
  if (shareUrl) {
    window.open(shareUrl, '_blank', 'width=600,height=400')
  }
}
</script>

<style scoped>
.noticia-page {
  background: var(--cor-branco);
  padding: 20px;
  min-height: 100vh;
}

/* CARD PRINCIPAL */
.noticia-card {
  max-width: 1200px;
  margin: 30px auto;
  background: var(--cor-branco);
  border-radius: 0px 0px 20px 20px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(8, 4, 4, 0.20);
}

/*  CARROSSEL */
.carousel-container {
  position: relative;
  width: 100%;
  background: var(--cor-cinza);
}

.carousel-main {
  position: relative;
  width: 100%;
  height: 650px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  cursor: zoom-in;
  transition: filter 0.3s ease;
}

.carousel-image:hover {
  filter: brightness(1.05);
}

/* BOTÕES DE NAVEGAÇÃO */
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(63, 55, 55, 0.25);
  border: none;
  font-size: var(--f4);
  width: 60px;
  height: 60px;
  border-radius: 20%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  transition: all 0.3s ease;
  backdrop-filter: blur(8px);
}

.carousel-btn:hover {
  background: rgba(255, 255, 255, 0.45);
  transform: translateY(-50%) scale(1.1);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
}

.carousel-prev {
  left: 20px;
}

.carousel-next {
  right: 20px;
}

/* INDICADOR DE IMAGEM ATUAL */
.carousel-info {
  position: absolute;
  bottom: 20px;
  left: 20px;
  background: rgba(0, 0, 0, 0.5);
  color: var(--cor-branco);
  padding: 8px 16px;
  border-radius: 20px;
  font-size: var(--f2);
  font-family: bold;
  backdrop-filter: blur(8px);
  z-index: 10;
}

/* PONTOS INDICADORES */
.carousel-dots {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 10px;
  z-index: 10;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.4);
  cursor: pointer;
  transition: all 0.3s ease;
}

.dot:hover {
  background: rgba(255, 255, 255, 0.7);
  transform: scale(1.2);
}

.dot.active {
  width: 32px;
  border-radius: 6px;
  background: var(--cor-verde);
}

/*  MODAL IMAGEM  */
.imagem-modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  padding: 20px;
  backdrop-filter: blur(5px);
}

.modal-content {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  max-width: 90vw;
}

.imagem-modal-conteudo {
  max-width: 100%;
  max-height: 85vh;
  object-fit: contain;
  border-radius: 8px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.8);
  animation: zoomIn 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
}

@keyframes zoomIn {
  from {
    opacity: 0;
    transform: scale(0.85);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* BOTÕES NO MODAL */
.modal-prev,
.modal-next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.2);
  border: none;
  font-size: 40px;
  width: 70px;
  height: 70px;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  backdrop-filter: blur(8px);
  z-index: 10001;
}



.modal-prev:hover,
.modal-next:hover {
  background: rgba(255, 255, 255, 0.35);
  transform: translateY(-50%) scale(1.15);
  box-shadow: 0 10px 30px rgba(255, 255, 255, 0.2);
}

.modal-prev {
  left: -90px;
}

.modal-next {
  right: -90px;
}

/* BOTÃO FECHAR */
.modal-fechar {
  position: absolute;
  top: -60px;
  right: 0;
  background: transparent;
  border: none;
  color: #ffffff;
  font-size: 40px;
  cursor: pointer;
  line-height: 1;
  transition: all 0.2s ease;
  z-index: 10002;
}

.modal-fechar:hover {
  transform: scale(1.2) rotate(90deg);
  opacity: 0.8;
}

/* INDICADOR NO MODAL */
.modal-indicator {
  position: absolute;
  bottom: -50px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(255, 255, 255, 0.15);
  color: white;
  padding: 10px 20px;
  border-radius: 20px;
  font-size: 15px;
  font-weight: 600;
  backdrop-filter: blur(8px);
}

/* CONTEÚDO */
.card-conteudo {
  padding: 32px;
}

/* DATA */
.card-data {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: var(--f3);
  color: var(--cor-vermelha);
  font-family: Regular;
  margin-bottom: var(--f9);
}

/* TÍTULO */
.card-titulo {
  font-size: var(--f4);
  line-height: 1.3;
  color: var(--cor-preta);
  margin-bottom: var(--f9);
  font-family: bold;
}

.card-subtitulo {
  padding: 10px 2px;
  margin-bottom: var(--f9);
  font-size: var(--f3);
  color: var(--cor-preta);
  font-family: semibold;
}

.card-texto p {
  font-size: var(--f3);
  line-height: 1.8;
  color: var(--cor-preta);
  text-align: justify;
  font-family: Regular;
}

/* COMPARTILHAR */
.card-compartilhar {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin: 32px 0;
}

.share {
  width: 100%;
  height: 55px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.25s ease, opacity 0.25s ease;
}

.share svg {
  width: 35%;
  height: 22px;
}

svg {
  width: 18px;
}

.share:hover {
  transform: translateY(-3px);
  opacity: 0.9;
}

.whatsapp {
  border: 2px solid #25d366; 
  background: var(--cor-branco);
}

.facebook {
  border: 2px solid #1877f2;
  background: var(--cor-branco);
}

.instagram {
   border: 2px solid #e1306c;
   background: var(--cor-branco);
}

.linkedin {
  border: 2px solid #0a66c2;
  background: var(--cor-branco);
}

/* BOTÃO OFICIAL */
.card-oficial {
  text-align: center;
}

.btn-oficial {
  background: var(--cor-vermelha);
  color: var(--cor-branco);
  border: none;
  padding: 12px 28px;
  border-radius: 8px;
  font-size: var(--f3);
  font-family: semibold;
}

/* TRANSIÇÕES */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-to,
.fade-leave-from {
  opacity: 1;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
  backdrop-filter: blur(0px);
}

.modal-fade-enter-to,
.modal-fade-leave-from {
  opacity: 1;
  backdrop-filter: blur(5px);
}

/* SEM DADO */
.sem-dado {
  text-align: center;
  padding: 60px 20px;
  color: var(--cor-preta);
}

/* RESPONSIVO */
@media (max-width: 768px) {
  .carousel-main {
    height: 300px;
  }

  .carousel-btn {
    width: 45px;
    height: 45px;
    font-size: 24px;
  }

  .carousel-prev {
    left: 10px;
  }

  .carousel-next {
    right: 10px;
  }

  .modal-prev,
  .modal-next {
    width: 50px;
    height: 50px;
    font-size: 24px;
  }

  .modal-prev {
    left: 10px;
    position: relative;
  }

  .modal-next {
    right: 10px;
    position: relative;
  }

  .modal-fechar {
    top: 10px;
    right: 10px;
  }

  .card-conteudo {
    padding: 20px;
  }

  .card-titulo {
    font-size: 1.5rem;
  }

  .carousel-dots {
    gap: 8px;
  }

  .dot {
    width: 10px;
    height: 10px;
  }

  .dot.active {
    width: 28px;
  }
}
</style>