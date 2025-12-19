<template>
  <div class="legislacao">
    <Legislacao1Section/>
  <Herolegislacao/>
  <Legislacao2Section/>
  <Herolegislacao2 />
  
</div>
 
</template>

<script>
import Herolegislacao from '@/components/legislacao/Herolegislacao.vue';
import Herolegislacao2 from '@/components/legislacao/Herolegislacao2.vue';
import Legislacao1Section from '@/components/legislacao/Legislacao1Section.vue';
import Legislacao2Section from '@/components/legislacao/Legislacao2Section.vue';


export default {
  name: 'legislacao',
  components: {
    Herolegislacao,
    Legislacao1Section,
    Legislacao2Section,
    Herolegislacao2,
  }
}

</script>


