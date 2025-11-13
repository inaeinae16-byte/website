<template>
  <div class="home">
    <HeroSection />
    <Sectionfaixa />
    <Sectioninspecoes />
    <SectionAreadeAtuação />
    <SectionNoticias />
  </div>
</template>

<script>
import HeroSection from '@/components/home/HeroSection.vue'
import Sectionfaixa from '@/components/home/Sectionfaixa.vue'
import Sectioninspecoes from '@/components/home/Sectioninspecoes.vue'
import SectionAreadeAtuação from '@/components/home/SectionAreadeAtuação.vue'
import SectionNoticias from '@/components/home/SectionNoticias.vue'

export default {
  name: 'HomePage',
  components: {
    HeroSection,
    Sectionfaixa,
    Sectioninspecoes,
    SectionAreadeAtuação,
    SectionNoticias
  }
}
</script>

<style scoped></style>