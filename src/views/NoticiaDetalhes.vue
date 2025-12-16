<template>
  <div class="noticia-detalhe">
    <div v-if="noticia" class="detalhe-wrap">
      <!-- Imagem de destaque -->
      <div class="detalhe-imagem-container">
        <img :src="noticia.imagem" :alt="noticia.titulo" class="detalhe-imagem" />
      </div>

      <!-- Conteúdo principal -->
      <main class="detalhe-conteudo container">
        <!-- Card branco com todo o conteúdo -->
        <div class="content-card">
          <!-- Cabeçalho com data e visualizações -->
          <div class="detalhe-header">
            <div class="info-item">
              <Svg name="iconcalendario" />
              <span> Sexta-feira, {{ noticia.data || '28 de Setembro 2025' }}</span>
            </div>
          </div>

          <!-- Título -->
          <h1 class="detalhe-titulo">{{ noticia.titulo }}</h1>

          <!-- Subtítulo/Resumo -->
          <div class="detalhe-subtitulo">
            <strong>{{ noticia.subtitulo || 'INAE RECEBE VISITA DO PROCURADOR-GERAL DA REPÚBLICA' }}</strong>
          </div>

          <!-- Conteúdo do artigo -->
          <article class="detalhe-artigo">
            <p class="detalhe-texto">{{ noticia.descricao }}</p>
          </article>

          <!-- Botões de compartilhamento -->
          <div class="compartilhar-section">
            <button class="btn-compartilhar whatsapp" @click="compartilhar('whatsapp')" title="Compartilhar no WhatsApp">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
              </svg>
            </button>
            <button class="btn-compartilhar facebook" @click="compartilhar('facebook')" title="Compartilhar no Facebook">
              <Svg name="iconFB" />
            </button>
            <button class="btn-compartilhar instagram" @click="compartilhar('instagram')" title="Compartilhar no Instagram">
              <Svg name="iconIG" />
            </button>
            <button class="btn-compartilhar linkedin" @click="compartilhar('linkedin')" title="Compartilhar no LinkedIn">
              <Svg name="iconlinkdin" />
            </button>
          </div>

          <!-- Botão notícia oficial -->
          <div class="noticia-oficial-section">
            <button class="btn-noticia-oficial">
              <svg viewBox="0 0 24 24" fill="currentColor" width="16" height="16">
                <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-5 14H7v-2h7v2zm3-4H7v-2h10v2zm0-4H7V7h10v2z"/>
              </svg>
              Notícia oficial
            </button>
          </div>
        </div>

        <!-- Botão voltar -->
        <div class="voltar-section">
          <button class="btn-voltar-bottom" @click="voltar">Voltar</button>
        </div>
      </main>
    </div>

    <div v-else class="sem-dado container">
      <p>Notícia não encontrada. Volte para a lista de notícias.</p>
      <button class="btn-voltar" @click="voltar">Voltar às Notícias</button>
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
</script>

<style scoped>
.noticia-detalhe {
  background: #fff;
  min-height: 100vh;
}

.detalhe-imagem-container {
  width: 100%;
  max-height: 400px;
  overflow: hidden;
  background: #f5f5f5;
}

.detalhe-imagem {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center top;
  display: block;
}

.detalhe-conteudo {
  max-width: 900px;
  margin: 0 auto;
  padding: 30px 20px 80px;
}

.detalhe-header {
  display: flex;
  gap: 24px;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #e63946;
  font-size: 14px;
}

.icon {
  width: 18px;
  height: 18px;
  color: #e63946;
}

.detalhe-titulo {
  font-size: 1.8rem;
  color: #1a1a1a;
  margin: 0 0 20px 0;
  line-height: 1.3;
  font-weight: 600;
}

.detalhe-subtitulo {
  background: #f8f9fa;
  padding: 16px;
  margin-bottom: 24px;
  border-radius: 4px;
  font-size: 15px;
  color: #2c3e50;
}

.detalhe-artigo {
  margin-bottom: 32px;
}

.detalhe-texto {
  font-size: 16px;
  line-height: 1.8;
  color: #4a5568;
  margin: 0;
  text-align: justify;
}

.compartilhar-section {
  display: flex;
  gap: 12px;
  margin-bottom: 24px;
  padding: 20px 0;
  border-top: 1px solid #e5e7eb;
  border-bottom: 1px solid #e5e7eb;
}

.btn-compartilhar {
  width: 48px;
  height: 48px;
  border-radius: 8px;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.btn-compartilhar svg {
  width: 24px;
  height: 24px;
}

.btn-compartilhar.whatsapp {
  background: #25D366;
  color: white;
}

.btn-compartilhar.whatsapp:hover {
  background: #1fb855;
  transform: translateY(-2px);
}

.btn-compartilhar.facebook {


}

.btn-compartilhar.facebook:hover {
  background: #0d65d9;
  transform: translateY(-2px);
}

.btn-compartilhar.instagram {

}

.btn-compartilhar.instagram:hover {
  transform: translateY(-2px);
  opacity: 0.9;
}

.btn-compartilhar.linkedin {
  color: white;
}

.btn-compartilhar.linkedin:hover {

  transform: translateY(-2px);
}

.noticia-oficial-section {
  margin-bottom: 32px;
}

.btn-noticia-oficial {
  background: #e63946;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  transition: background 0.3s ease;
}

.btn-noticia-oficial:hover {
  background: #d62839;
}

.voltar-section {
  margin-top: 40px;
}

.btn-voltar-bottom {
  background: transparent;
  color: #2563eb;
  border: 2px solid #2563eb;
  padding: 10px 24px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 15px;
  font-weight: 500;
  transition: all 0.3s ease;
}

.btn-voltar-bottom:hover {
  background: #2563eb;
  color: white;
}

.sem-dado {
  padding: 40px 20px;
  text-align: center;
}

.btn-voltar {
  background: #2563eb;
  color: white;
  border: none;
  padding: 10px 24px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 15px;
  margin-top: 16px;
}

@media (max-width: 768px) {
  .detalhe-titulo {
    font-size: 1.5rem;
  }
  
  .detalhe-header {
    flex-direction: column;
    gap: 12px;
  }
  
  .compartilhar-section {
    justify-content: center;
  }
}
</style>