<template>
  <section class="hero-banner">
    <div class="carousel">
      <!-- Slides -->
      <div
        v-for="(slide, index) in slides"
        :key="index"
        class="slide"
        :class="{ active: index === currentSlide }"
      >
        <!-- Fundo -->
        <div class="slide-bg" :style="{ backgroundImage: `url(${slide.image})` }"></div>
      </div>
    </div>

    <!-- Botões de Navegação (INFERIORES) -->
    <button class="nav-btn prev" @click="prevSlide">
      <Svg name="setaEsquerda" class="setaEsquerda" />
    </button>
    <button class="nav-btn next" @click="nextSlide">
      <Svg name="setaEsquerda" class="SetaDireita"/>
    </button>

    <!-- Indicadores -->
    <div class="dots">
      <span
        v-for="(slide, index) in slides"
        :key="index"
        :class="{ active: index === currentSlide }"
        @click="goToSlide(index)"
      ></span>
    </div>
  </section>
</template>

<script setup>
import Svg from '../../assets/Svg/Svgs.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue'

//As fotos
const slides = ref([
  {
    image: new URL('@/assets/banner01.png', import.meta.url).href
  },
  {
    image: new URL('@/assets/banner02.png', import.meta.url).href
  },
  {
    image: new URL('@/assets/banner03.png', import.meta.url).href
  }
])

const currentSlide = ref(0)
let interval = null

const startAutoPlay = () => {
  interval = setInterval(() => {
    currentSlide.value = (currentSlide.value + 1) % slides.value.length
  }, 5000)
}

const goToSlide = (index) => {
  currentSlide.value = index
  clearInterval(interval)
  startAutoPlay()
}

const prevSlide = () => {
  currentSlide.value = currentSlide.value === 0 ? slides.value.length - 1 : currentSlide.value - 1
  goToSlide(currentSlide.value)
}

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.value.length
  goToSlide(currentSlide.value)
}

onMounted(() => {
  startAutoPlay()
})

onBeforeUnmount(() => {
  clearInterval(interval)
})
</script>

<style scoped>
.hero-banner {
  position: relative;
  height: 600px;
  overflow: hidden;
}

.carousel {
  position: relative;
  width: 100%;
  height: 100%;
}

.slide {
  position: absolute;
  bottom: 60px;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 1.9s ease-in-out;
  display: flex;
  align-items: center;
}

.slide.active {
  opacity: 1;
  z-index: 1;
}

.slide-bg {
  position: absolute;
  top: 60px;
  left: 0;
  width: 100%;
  height: 600px;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  filter: brightness(0.75);
}

/* BOTÕES DE NAVEGAÇÃO INFERIORES */
.nav-btn {
  position: absolute;
  bottom: 50%;
  background-color: transparent;
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  z-index: 3;
  transition: all 0.3s ease;
  backdrop-filter: blur(8px);
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-btn:hover {
  background: rgba(255, 255, 255, 0.4);
}

.SetaDireita{
  transform: scale(-1);
}

.prev {
  left: 3rem;
}

.next {
  right: 3rem;
}
/* Indicadores */
.dots {
  position: absolute;
  bottom: 2.5rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 1rem;
  z-index: 3;
}

.dots span {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(255,255,255,0.5);
  cursor: pointer;
  transition: all 0.4s ease;
}

.dots span.active {
  background: var(--cor-verde);
  transform: scale(1.4);
}

/* Responsivo */
@media (max-width: 992px) {
  .hero-banner { height: 70vh; min-height: 360px;}
  .slide-content { padding: 2rem; max-width: 100%; text-align: center; }
  .slide-content h1 { font-size: 2.4rem; }
  .slide-content p { font-size: 1.1rem; }
  .btn-denuncia { padding: 0.9rem 1.8rem; font-size: 1rem; }
  .nav-btn { width: 45px; height: 45px; font-size: 1.2rem; }
  .prev { left: 1rem; }
  .next { right: 1rem; }
}

@media (max-width: 600px) {
  .hero-banner { height: 60vh; }
  .slide-content h1 { font-size: 2rem; }
  .slide-content p { font-size: 1rem; }
  .btn-denuncia { padding: 0.8rem 1.5rem; font-size: 0.95rem; }
  .nav-btn { width: 40px; height: 40px; font-size: 1.1rem; }
  .dots {bottom: 1.2rem; gap: 0.7rem;}
}
</style>