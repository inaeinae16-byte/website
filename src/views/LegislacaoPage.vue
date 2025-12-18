<template>
  <div class="legislacao">
    <Legislacao1Section/>
  <Herolegislacao/>
</div>
 
</template>

<script>
import Herolegislacao from '@/components/legislacao/Herolegislacao.vue';
import Legislacao1Section from '@/components/legislacao/Legislacao1Section.vue';


export default {
  name: 'legislacao',
  components: {
    Herolegislacao,
    Legislacao1Section,
  }
}

</script>


