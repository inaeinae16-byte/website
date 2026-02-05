<template>
  <!-- Container principal -->
  <div class="lideranca-container">
    
    <!-- Título principal -->
    <h1 class="titulo-principal">NOSSA LIDERANÇA</h1>

    <p class="paragrafo-principal">A INAE é dirigida por um Inspector-geral, e por um Inspector-geral Adjunto, ambos nomeados pelo Primeiro-ministro,
       sob proposta do ministro que superintende a área de indústria e comércio. 
      O mandato do Inspector-geral e Inspector-geral Adjunto é de cinco anos, renovável uma vez.</p>
    
    <!-- Grid de líderes -->
    <div class="lideres-grid">
      
      <!-- Card do primeiro líder -->
      <div class="lider-card">
        <!-- Container da imagem -->
        <div class="imagem-container">
          <img   :src="require('../../assets/inspetora.png')"   alt="Dra. Shaquila Abdulcar Mohomed"   class="foto-lider" />
        </div>
        
        <!-- Informações do líder -->
        <div class="info-container">
          <h3 class="nome-lider">DRA. SHAQUILA ABDULCAR MOHOMED</h3>
          <p class="cargo-lider">INSPECTORA-GERAL</p>
        </div>
      </div>

      <!-- Card do segundo líder -->
      <div class="lider-card">
        <!-- Container da imagem -->
        <div class="imagem-container">
          <img :src="require('../../assets/inspetor-semfundo.png')" alt="Dr. Eduardo Muchanissso Samuel Jane" class="foto-lider"/>
        </div>
        
        <!-- Informações do líder -->
        <div class="info-container">
          <h3 class="nome-lider">DR. EDUARDO MUCHANISSSO SAMUEL JANE</h3>
          <p class="cargo-lider">INSPECTOR-GERAL ADJUNTO</p>
        </div>
      </div>

    </div>
  </div>
</template>



<style scoped>

.lideranca-container {
  width: 100%;
  max-width: 1200px;
  margin: 60px auto;
  padding: 40px 20px;

}

.titulo-principal {
  text-align: center;
  color: var(--cor-verde);
  font-size: var(--f5);
  font-family: bold;
  margin-bottom: 50px;
}

.paragrafo-principal {
  text-align: center;
  color: var(--cor-preto);
  font-size: var(--f3);
  font-family: semibold;
  margin-bottom: 90px;
  line-height: 200%;
  padding: 0px 180px 0px 267px;
}

/* Grid responsivo para os cards */
.lideres-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 60px;
  max-width: 1000px;
  margin: 0 auto;
}

/* Card individual de cada líder */
.lider-card {
  background-color: var(--cor-verde);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

/* Efeito hover no card */
.lider-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
}

/* Container da imagem */
.imagem-container {
  width: 100%;
  height: 545px;
  overflow: hidden;
}

/* Foto do líder */
.foto-lider {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
}

/* Container das informações */
.info-container {
  padding: 20px;
  background-color: #d1d5db;
  text-align: center;
}

/* Nome do líder */
.nome-lider {
  font-size: var(--f3);
  font-family: bold;
  color: var(--cor-preto);
  line-height: 1.4;
  margin-bottom: 10px;
}

/* Cargo do líder */
.cargo-lider {
  font-size: var(--f2);
  font-family: bold;
  color: var(--cor-preto);
  margin: 0;
  letter-spacing: 0.3px;
}

/* Responsividade para tablets */
@media (max-width: 768px) {
  .titulo-principal {
    font-size: 24px;
    margin-bottom: 40px;
  }

  .lideres-grid {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .imagem-container {
    height: 250px;
  }
}

/* Responsividade para mobile */
@media (max-width: 480px) {
  .lideranca-container {
    padding: 30px 15px;
  }

  .titulo-principal {
    font-size: 20px;
    margin-bottom: 30px;
  }

  .lideres-grid {
    gap: 20px;
  }

  .imagem-container {
    height: 280px;
  }

  .nome-lider {
    font-size: 13px;
  }

  .cargo-lider {
    font-size: 12px;
  }
}
</style>