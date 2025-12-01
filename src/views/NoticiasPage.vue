<template>
<div class="Noticias">
<HeroNoticias />
<SlideUltimasnoticias />
</div>
</template>

<script>
import HeroNoticias from '@/components/noticias/HeroNoticias.vue';
import SlideUltimasnoticias from '@/components/noticias/slideUltimasnoticias.vue';

export default {
    name: 'Noticias',
    components: {
        HeroNoticias,
        SlideUltimasnoticias,
    }
}
</script>

<style scoped></style>
