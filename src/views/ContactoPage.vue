<template>
  <div class="contacto">
 <ContactoHero />   
 <Perguntas />
 <Delegacoes />
 
  </div>
</template>

<script>
import ContactoHero from '@/components/contacto/ContactoHero.vue';
import Perguntas from '@/components/contacto/Perguntas.vue';
import Delegacoes from '@/components/contacto/Delegacoes.vue';


  export default {
    name: 'contacto',
    components: {
      ContactoHero,
      Perguntas,
      Delegacoes,
    }
  }

</script>