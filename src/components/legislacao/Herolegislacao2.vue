<template>
  <section class="container-geral">
    <div class="card-legislacao">

      <div class="coluna-esquerda">
        
        <Svg name="iconFuncionamentoinae" class="icone-principal"/>
      </div>

      <div class="coluna-direita">
        <ul class="lista-documentos">
          
          <li
            v-for="(doc, index) in documentos"
            :key="index"
            class="item-documento">
            <a :href="doc.pdf" target="_blank" rel="noopener" class="link-documento" >
              <Svg name="iconpdf" class="icone-pdf" />
              {{ doc.titulo }}
            </a>
          </li>
        </ul>
      </div>

    </div>
  </section>
</template>

<style scoped>
.container-geral {
 max-width: 1200px;
  margin:30px auto;
}

/* CARD PRINCIPAL */
.card-legislacao {
  display: grid;
  grid-template-columns: 1fr 2fr;
  background: #f0f6f2;
  border-radius: 0px 20px 20px 20px ;
  overflow: hidden;
}


.coluna-esquerda {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 60px;
    background: var(--cor-branco);
    border: 2px solid #28782e;
    border-radius:0px 0px 0px 20px ;
}

.icone-principal {
  width: 140px;
  color: var(--cor-verde);
}

/* COLUNA DIREITA */
.coluna-direita {
    padding: 120px;
}

/* LISTA DE DOCUMENTOS */
.lista-documentos {
  list-style: none;
  padding: 0;
  margin: 0;
}

.item-documento {
  margin-bottom: 16px;
}

/* LINK DO PDF */
.link-documento {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
  color: #2f7d4e;
  font-family: semibold;
  font-size: var(--f3);
  transition: all 0.3s ease;
}

.link-documento:hover {
  transform: translateX(6px);
}

/* ÍCONE PDF */
.icone-pdf {
  width: 26px;
  color: #e53935;
}

/* RESPONSIVO */
@media (max-width: 768px) {
  .card-legislacao {
    grid-template-columns: 1fr;
  }

  .coluna-esquerda {
    border-right: none;
  }

  .coluna-direita {
    padding: 150px;
    margin: -100px;
}

 
}

</style>

<script setup>
    import Svg from '../../assets/Svg/Svgs.vue'

const documentos = [
  {
    titulo: "Criação da INAE",
    pdf: "https://drive.google.com/file/d/1S1tWo3ApLrCIV4n4Ho-B8Mfh2mvVBQd3/view?usp=sharing",
  },
  {
    titulo: "Revisão da criação da INAE",
    pdf: "https://drive.google.com/file/d/1Y80xb3A7TjtZUpP-kASzbXJ0qsBIrq98/view?usp=sharing",
  },
  {
    titulo: "Estudo orgânico da INAE",
    pdf: "https://drive.google.com/file/d/1DxEpzgtXr03MnfrZZQwDWP5neWIx1dxS/view?usp=sharing",
  },
  {
    titulo: "Regulamento interno da INAE",
    pdf: "https://drive.google.com/file/d/1qbwzrVP2KWbA9Vx43zktFrAz4du4t5g4/view?usp=sharing",
  },
  {
    titulo: "Carreiras e funções específicas da INAE",
    pdf: "https://drive.google.com/file/d/1xcA8XzJuUmqm2vNyxHnLqpq9Hh6VGuRD/view?usp=sharing",
  },
]
</script>

