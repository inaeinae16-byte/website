<template>
 <div class="NaturezaSection">
   <CompetenciasSection/>
    <NaturezaSection/>
    <LiderancaSection/>
    <SectionAreadeAtuação/>
    <EstatutoOrganico />

 </div>
</template>

<script>
import NaturezaSection from '@/components/sobre-nos/NaturezaSection.vue';
import CompetenciasSection from '@/components/sobre-nos/CompetenciasSection.vue';
import LiderancaSection from '@/components/sobre-nos/lideranca-section.vue';
import SectionAreadeAtuação from '@/components/home/SectionAreadeAtuação.vue';
import EstatutoOrganico from '@/components/sobre-nos/EstatutoOrganico.vue';

export default {
  name: 'SobrePage',
  components: {
    CompetenciasSection,
    NaturezaSection,
    LiderancaSection,
    SectionAreadeAtuação,
    EstatutoOrganico
  }
}

</script>


