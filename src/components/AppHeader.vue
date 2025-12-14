<template>
  <header>
    <div class="baselogo">
      <Svg name="baselogo" class="baselogo" />
    </div>

    <div class="logoo">
      <Svg name="logo" class="logo1" />
    </div>

    <nav class="navbar">
       <ul class="nav-links" :class="{ 'mobile-open': mobileMenuOpen }">
        <li><router-link to="/" active-class="active" exact @click="closeMenu">Início</router-link></li>
        <li><router-link to="/sobre" active-class="active" exact @click="closeMenu">Sobre-Nós</router-link></li>
        <li><router-link to="/legislacao" active-class="active" exact @click="closeMenu">Legislação</router-link></li>
        <li><router-link to="/noticias" active-class="active" exact @click="closeMenu">Notícias</router-link></li>
        <li><router-link to="/concursos" active-class="active" exact @click="closeMenu">Concursos</router-link></li>
        <li><router-link to="/contacto" active-class="active" exact @click="closeMenu">Contacto</router-link></li>
      </ul>
    </nav>

    <!--BOTAO HUMBÚRGUER -->
    <!-- BOTÃO HAMBÚRGUER - Aparece apenas em mobile (< 998px) -->
    <button 
      class="hamburger-button"
      :class="{ 'hamburger-active': mobileMenuOpen }"
      @click="toggleMobileMenu"
      aria-label="Toggle menu"
    >
      <!-- span de humburger -->
      <span class="hamburger-line"></span>
      <span class="hamburger-line"></span>
    </button>

    <!-- Abre de cima para baixo quando ativado -->
    <div 
      class="mobile-menu"
      :class="{ 'mobile-menu-open': mobileMenuOpen }"
    >

      <ul class="mobile-nav-links">
        <li><router-link to="/" active-class="active" exact @click="closeMenu">Início</router-link></li>
        <li><router-link to="/sobre" active-class="active" exact @click="closeMenu">Sobre-Nós</router-link></li>
        <li><router-link to="/legislacao" active-class="active" exact @click="closeMenu">Legislação</router-link></li>
        <li><router-link to="/noticias" active-class="active" exact @click="closeMenu">Notícias</router-link></li>
        <li><router-link to="/concursos" active-class="active" exact @click="closeMenu">Concursos</router-link></li>
        <li><router-link to="/contacto" active-class="active" exact @click="closeMenu">Contacto</router-link></li>
      </ul>

      <!-- Botão de denúncia dentro do menu mobile -->
      <button class="Buttondenuncia-mobile" @click="$router.push('/denuncia')">
        <Svg name="denuncia" class="denuncia"/> Denuncia 
      </button>
    </div>
 
    <!--Button desktop-->
    <!-- <router-link to="/concursos" active-class="active" exact @click="closeMenu">Concursos</router-link></li> -->
     <button class="Buttondenuncia" @click="$router.push('/denuncia')" >
    <Svg name="denuncia" class="denuncia"/> Denuncia 
    </button>

  </header>
  
</template>

<script setup>
import { ref } from 'vue'
import Svg from '../assets/Svg/Svgs.vue'

//controla o estado do menu moblie se esta aperto ou fechado ~
const mobileMenuOpen = ref (false)

//funcao para alternar o menu mobile
const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

//Funcao para fechar o menu quando clicas num link 
const closeMenu = () => {
  mobileMenuOpen.value = false
}
</script>

<style scoped>
header {
  display: flex;
  width: 100%;
  height: 60px;
  background-color: var(--cor-verde);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
  align-items: center;
}

.baselogo {
  width: 286px;
  height: 60px;
  right: 51px;
}

.navbar {
  display: flex;
  justify-content: center;
  text-align: center;
  width: 100%;
  position: fixed;
}

ul {
  display: flex;
  align-items: center;
  text-decoration: none;
  list-style: none;
}

li {
  font-family: semibold;
  font-size: var(--f3);
  padding: 1.5rem;
  list-style: none;
  color: var(--cor-branco);
  transition: all .1s;
}

li a {
  color: var(--cor-branco);
  text-decoration: none;
}

li a:hover{
  opacity: .8;
}

.logo1{
  width: 40px;
  height: 60px;
  right: 230px;
}

.Buttondenuncia{
  cursor: pointer;
  display: flex;
  text-align: center;
  background-color: var(--cor-branco);
  color: var(--cor-preto);
  font-family: semibold;
  margin-left: auto;
  margin-right: 50px;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  gap: 2px;
  transition: .5s ease-in-out;
  z-index: 100;
}

.Buttondenuncia:hover {
  background-color: var(--cor-vermelha);
  color: var(--cor-branco);
}

.denuncia {
  width: 15px;
  color: var(--cor-branco);
}

/* Menu Hamburguer esconde no desktop*/

.hamburger-button {
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  background: none;
  border: none;
  cursor: pointer;
  margin-left: auto;
  margin-right: 25px;
  z-index: 1001;
  gap: 6px;
}

.hamburger-line {
  width: 50px;
  height: 2px;
  background-color: var(--cor-branco);
  border-radius: 2px;
  transition: all 0.3s ease-in-out;
}

 .hamburger-line:nth-child(2){
 transform-origin:right;
  transform: scaleX(0.6);
 }

/*Efeito x */
.hamburger-button.hamburger-active .hamburger-line:nth-child(1) {
  transform: rotate(45deg) translateY(10px);
  width: 40px;
}

.hamburger-button.hamburger-active .hamburger-line:nth-child(2) {
  transform: rotate(-45deg) translateY(-25px);
  width: 40px;
}

/* hamburger mobile */
.mobile-menu {
  position: fixed;
  top: 60px;
  left: 0;
  right: 0;
  background-color: var(--cor-verde);
  transform: translateY(-120%);
  transition: transform 0.4s ease-in-out;
  z-index: 999;
}

.mobile-menu.mobile-menu-open {
  transform: translateY(0);
}


 .mobile-nav-links {
  display: flex;
  flex-direction: column;
  list-style: none;
  padding: 0;
  margin: 0;
 }

  .mobile-nav-links li {
    padding: 15px 20px;
    border-bottom: 1px solid var(--cor-verde);
    text-align: left;
  }

   .mobile-nav-links li a {
    color: var(--cor-branco);
    font-family: semibold;
    font-size: var(--f3);
   }

   .mobile-nav-links li a:hover {
    opacity: 0.8;
   }

   
/* Botão de denúncia dentro do menu mobile */
.Buttondenuncia-mobile {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: var(--cor-branco);
  color: var(--cor-preto);
  font-family: semibold;
  width: calc(100% - 40px);
  margin: 20px;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  gap: 8px;
  transition: .5s ease-in-out;
}

.Buttondenuncia-mobile:hover {
  background-color: var(--cor-vermelha);
  color: var(--cor-branco);
}


@media (max-width: 998px) {
  /* Esconde a navbar desktop */
  .navbar {
    display: none;
  }

  /* Mostra o botão hambúrguer */
  .hamburger-button {
    display: flex;
  }

  /* Esconde o botão de denúncia desktop */
  .Buttondenuncia {
    display: none;
  }
}





</style>