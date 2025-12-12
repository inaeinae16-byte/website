<template>
<div class="denuncia">
  <h1>Denuncie</h1>
  <p>Preencha os dados</p>
</div>

<section class="formulario">
  <div class="conteudo_principal">
    <form action="">
      <div class="campos">
        <fieldset>
          <legend>Seu nome <span class="obrigatorio">*</span></legend>
          <input type="text" placeholder="Ex:João" id="nome">
        </fieldset>

        <fieldset>
          <legend>E-mail<span class="obrigatorio">*</span></legend>
          <input type="email" placeholder="email@gmail.com" id="email" required>
        </fieldset>

        <fieldset>
          <legend>Contacto <span class="obrigatorio">*</span></legend>
          <input type="text" placeholder="+258" id="contacto">
        </fieldset>   

        <fieldset>
          <legend>Endereço <span class="obrigatorio">*</span></legend>
          <input type="text" placeholder="Digite o seu endereço" id="endereco">
        </fieldset>  
      </div>

      <h3>Dados da entidade econômica</h3>

      <div class="campos_entidade">
        <fieldset>
          <legend>Nome do estabelecimento <span class="obrigatorio">*</span></legend>
          <input type="text" id="estabelecimento">
        </fieldset>  

        <fieldset>
          <legend>Província<span class="obrigatorio">*</span></legend>
          <!-- <div class="select-wrapper">
            <select id="provincia">
              <option value="">Selecione a Província</option>
              <option value="maputo">Maputo</option>
              <option value="gaza">Gaza</option>
              <option value="inhambane">Inhambane</option>
              <option value="sofala">Sofala</option>
              <option value="manica">Manica</option>
              <option value="tete">Tete</option>
              <option value="zambezia">Zambézia</option>
              <option value="nampula">Nampula</option>
              <option value="cabo-delgado">Cabo Delgado</option>
              <option value="niassa">Niassa</option>
            </select>
          </div> -->
           <div class="select_option">
                {{ selectedTextProvincia }}

                <span :class="['arrow', { open: isOpen }]"></span>

              </div>
        </fieldset>  

        <fieldset>
          <legend>Localização do estabelecimento <span class="obrigatorio">*</span></legend>
          <input type="text" placeholder="Localização" id="localizacao">
        </fieldset>  

        <fieldset>
          <legend>Contacto do estabelecimento <span class="obrigatorio">*</span></legend>
          <input type="text" placeholder="+258" id="contacto_estabelecimento">
        </fieldset>
      </div>

      <div class="ultima">
        <fieldset class="campo-data">
          <legend>Data da corrência <span class="obrigatorio">*</span></legend>
          <input type="text" placeholder="dd/mm/aa" id="data_ocorrencia">
        </fieldset>

        <fieldset class="campo-assunto">
          <legend>Assunto <span class="obrigatorio">*</span></legend>
          <div class="select-wrapper">
            <!-- <select id="assunto">
              <option value="">Localização</option>
              <option value="preco">Preço abusivo</option>
              <option value="qualidade">Má qualidade</option>
              <option value="atendimento">Mau atendimento</option>
              <option value="higiene">Falta de higiene</option>
              <option value="outro">Outro</option>
            </select> -->

            <div class="customizar_select" @click="toggleSelect">
              <div class="select_option">
                {{ selectedText }}

                <span :class="['arrow', { open: isOpen }]"></span>

              </div>

              <ul v-if="isOpen" class="options">
                <li @click.stop="selectoption('Preço abusivo')" class="option">Preço abusivo</li>
                <li @click.stop="selectoption('Má qualidade')" class="option">Má qualidade</li>
                <li @click.stop="selectoption('Mau atendimento')" class="option">Mau atendimento</li>
                <li @click.stop="selectoption('Falta de higiene')" class="option">Falta de higiene</li>
                <li @click.stop="selectoption('Outro')" class="option">Outro</li>
              </ul>
            </div>
          </div>
        </fieldset>

        <fieldset class="campo-evidencias">
          <legend>Evidências <span class="obrigatorio">*</span></legend>
          <div class="file-input-wrapper">
            <input type="file" id="evidencias" accept="image/*,video/*,.pdf">
            <label for="evidencias">
              <span class="file-placeholder">Suba a evidência</span>
              <span class="file-icon"> <Svg name="iconfile" class="iconfile"/> </span>
            </label>
          </div>
        </fieldset>
      </div>

      <fieldset class="campo-mensagem">
        <legend>Mensagem <span class="obrigatorio">*</span></legend>
        <textarea id="mensagem" placeholder="Deixe a sua mensagem" rows="4"></textarea>
      </fieldset>

      <button type="submit" class="btn-enviar">
        <span class="check-icon"><Svg name="iconcheck" class="check" />  </span>
        Enviar mensagem
      </button>
    </form>
  </div>
</section>
</template>

<style scoped>

.denuncia {
  margin-top: 50px;
  padding: 40px 20px 20px;
  text-align: center;
}

.denuncia h1 {
  color: var(--cor-vermelha);
  font-size: var(--f6);
  font-family: bold;
  margin-bottom: 10px;
}

.denuncia p {
  color:var(--cor-preto);
  font-size: var(--f3);
  font-family: Regular;
}

.formulario {
  display: flex;
  justify-content: center;
  padding: 20px;
  min-height: 100vh;
}

.conteudo_principal {
  background: var(--cor-branco);
  border: 2px solid var(--cor-vermelha);
  border-radius: 20px;
  padding: 40px;
  max-width: 1000px;
  width: 100%;
}

form {
  width: 100%;
}

.campos {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30px;
  margin-bottom: 10px;
}

h3 {
  color: var(--cor-vermelha);
  font-size: var(--f4);
  font-family: Regular;
  margin-bottom: 30px;
}

.campos_entidade {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  margin-bottom: 20px;
}

.ultima {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-bottom: 20px;
}

fieldset {
  border: 1px solid var(--cor-cinza);
  font-family: Regular;
  border-radius: 17px;
  padding: 2px 0px 10px 20px;
  position: relative;
  transition: all 0.3s ease;
}

fieldset:focus-within {
  border-color: var(--cor-vermelha);
}

legend {
  color: var(--cor-preto);
  font-size: var(--f3);
}

.obrigatorio {
  color: #e31e24;
  margin-left: 10px;
}

input[type="text"],
input[type="email"],
input[type="number"],
input[type="date"],
select,
textarea {
  width: 100%;
  padding: 10px 0;
  border: none;
  font-size: var(--f2);
  color: var(--cor-preto);
  transition: all 0.3s ease;
}

input::placeholder,
textarea::placeholder {
  color: var(--cor-cinza);
}

input:focus,
select:focus,
textarea:focus {
  outline: none;
}

/* Select customizado */
.select-wrapper {
  
}

.customizar_select {
  width: 100%;
  position: relative;
  cursor: pointer;
  font-family: Regular;
}

.select_option {
  width: 100%;
  background: var(--cor-branco);
  border: none;
  padding: 12px 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}


.arrow {
  width: 10px;
  height: 10px;
  border-right: 2px solid var(--cor-cinza);
  border-bottom: 2px solid var(--cor-cinza);
  transform: rotate(45deg);
  transition: 0.3s ease-in;
}

.arrow.open {
  transform: rotate(-135deg);
}

.options {
  list-style: none;
  position: absolute;
  top: 55px;
  left: 0;
  right: 0;
  background: var(--cor-branco);
  border-radius: 10px;
  border: 1px solid var(--cor-vermelha);
  z-index: 20;
}

.option {
  padding: 12px 16px;
}

.option:last-child {
  border-bottom: none;
}

.option:hover {
  color: var(--cor-cinza);
}


select {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  cursor: pointer;
  padding-right: 30px;
}
/*Ainda preciso avaliar */
select option {
  background-color: white;
  color: #333;
  padding: 10px;
}

/* File input customizado */
.file-input-wrapper {
  position: relative;
  width: 100%;
}

.file-input-wrapper input[type="file"] {
  position: absolute;
  opacity: 0;
  width: 100%;
  height: 100%;
  cursor: pointer;
  z-index: 2;
}

.file-input-wrapper label {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 0;
  cursor: pointer;
  transition: all 0.3s ease;
}

.file-placeholder {
  color: var(--cor-cinza);
  font-size: var(--f2);
}

.file-icon {
  font-size: 18px;
}

.iconfile {
  width: 20px;
  right: 20px;
}

/* Textarea */
textarea {
  resize: none;
  min-height: 10px;
  font-family: inherit;
  padding: 2px 0;
  margin-bottom: 40px;
}

.campo-mensagem {
  grid-column: 1 / -1;
}

/* Botão de enviar */
.btn-enviar {
  background-color: var(--cor-vermelha);
  color: var(--cor-branco);
  border: none;
  border-radius: 8px;
  padding: 17px 50px;
  font-size: var(--f9);
  font-family: Regular;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 20px;
  margin-left: auto;
  margin-top: 20px;
  transition: all 0.3s ease;
}

.btn-enviar:hover {
  background-color: #de3c42;
  transform: translateY(-2px);
}

.btn-enviar:active {
  transform: translateY(0);
}

.check-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 30px;
  background-color: var(--cor-preto);
  border-radius: 4px;
}
.check {
  width: 15px;
}

/* Responsividade */
@media (max-width: 768px) {
  .campos,
  .campos_entidade {
    grid-template-columns: 1fr;
  }

  .ultima {
    grid-template-columns: 1fr;
  }

  .conteudo_principal {
    padding: 20px;
  }

  .denuncia h1 {
    font-size: 36px;
  }
  
  h3{
    font-size: var(--f3);
  }

  .btn-enviar {
    font-size: var(--f3);
  }

}
</style>

<script setup>
  import Svg from '../../assets/Svg/Svgs.vue'

  import {  ref } from "vue";
  const isOpen = ref(false);
  const selectedText = ref("Selecione o assunto");
  const selectedTextProvincia = ref ("Selecione a Provincia");
 
  const toggleSelect = () => {
    isOpen.value = !isOpen.value
  };

  const selectoption = (texto) => {
    selectedText.value = texto;
    isOpen.value = false
  };
</script>