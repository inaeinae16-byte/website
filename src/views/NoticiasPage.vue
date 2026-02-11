<template>
<div class="Noticias">
<HeroNoticias />
<SectionNoticias />

<!-- <SlideUltimasnoticias /> -->
</div>
</template>

<script>
import SectionNoticias from '@/components/home/SectionNoticias.vue';
import HeroNoticias from '@/components/noticias/HeroNoticias.vue';
// import SlideUltimasnoticias from '@/components/noticias/slideUltimasnoticias.vue';

export default {
    name: 'Noticias',
    components: {
        HeroNoticias,
        SectionNoticias,
        // SlideUltimasnoticias,
    }
}
</script>

<style scoped></style>
