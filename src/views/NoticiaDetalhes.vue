<template>
  <div class="noticia-page">
    <div v-if="noticia" class="noticia-card">
     <!-- Imagem -->
      <div class="card-imagem" @click="abrirImagem">
        <img :src="noticia.imagem" :alt="noticia.titulo" />
      </div>

      <!-- MODAL IMAGEM -->
            <div v-if="imagemAberta" class="imagem-modal" @click.self="fecharImagem">
              <button class="modal-fechar" @click="fecharImagem">✕</button>
              <img :src="noticia.imagem" :alt="noticia.titulo" class="imagem-modal-conteudo" />
            </div>

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
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import Svg from '../assets/Svg/Svgs.vue'

const router = useRouter()
const noticia = ref(null)

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
})

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
      // Instagram não suporta compartilhamento direto via URL, então copiamos o link
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
//Clicar na imagem para ampliar
const imagemAberta = ref(false)

const abrirImagem = () => {
  imagemAberta.value = true
  document.body.style.overflow = 'hidden'
}

const fecharImagem = () => {
  imagemAberta.value = false
  document.body.style.overflow = ''
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

/* IMAGEM */
.card-imagem img {
  width: 100%;
  height: 650px;
  object-fit: cover;
  display: block;
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

/* MODAL IMAGEM */
.imagem-modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
  padding: 20px;
}

/* IMAGEM NO MODAL */
.imagem-modal-conteudo {
  max-width: 95%;
  max-height: 90vh;
  object-fit: contain;
  border-radius: 6px;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.6);
}

/* BOTÃO FECHAR */
.modal-fechar {
  position: absolute;
  top: 20px;
  right: 24px;
  background: transparent;
  border: none;
  color: #ffffff;
  font-size: 32px;
  cursor: pointer;
  line-height: 1;
  transition: transform 0.2s ease, opacity 0.2s ease;
}

.modal-fechar:hover {
  transform: scale(1.15);
  opacity: 0.8;
}

/* CURSOR NA IMAGEM */
.card-imagem {
  cursor: zoom-in;
}


/* RESPONSIVO */
@media (max-width: 768px) {
  .card-imagem img {
    height: 260px;
  }

  .card-conteudo {
    padding: 20px;
  }

  .card-titulo {
    font-size: 1.5rem;
  }
}

</style>