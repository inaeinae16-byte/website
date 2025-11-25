<template>
<div class="Legislacao1Section">
    <Legislacao1Section />
    <Section2 />
</div>
</template>

<script>

import Legislacao1Section from '@/components/Legislacao/Legislacao1Section.vue';
import Section2 from '@/components/Legislacao/Section2.vue';

export default {
    name: 'Legislacao',
    components: {
        Legislacao1Section,
        Section2,
    }
}
</script>