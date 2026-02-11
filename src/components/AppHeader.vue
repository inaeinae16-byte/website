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
        <!-- <li><router-link to="/concursos" active-class="active" exact @click="closeMenu">Concursos</router-link></li> Ainda nao há conteudo pra aqui  -->
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
        <!-- <li><router-link to="/concursos" active-class="active" exact @click="closeMenu">Concursos</router-link></li> -->
        <li><router-link to="/contacto" active-class="active" exact @click="closeMenu">Contacto</router-link></li>
      </ul>

      <!-- Botão de denúncia dentro do menu mobile -->
      <button class="Buttondenuncia-mobile" @click="() => { closeMenu(); $router.push('/denuncia') }">                                                                                                                                 
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
  position: sticky;
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


/* Tablets e telas médias */
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

/* Tablets pequenos */
@media (max-width: 768px) {
  .logo1 {
    width: 35px;
    height: 50px;
    right: 180px;
  }

  .hamburger-button {
    width: 45px;
    height: 45px;
    margin-right: 15px;
  }

  .hamburger-line {
    width: 40px;
  }

  .mobile-nav-links li {
    padding: 14px 18px;
  }

  .mobile-nav-links li a {
    font-size: 15px;
  }

  .Buttondenuncia-mobile {
    width: calc(100% - 36px);
    margin: 18px;
    padding: 12px 18px;
    font-size: 15px;
  }
}

/* Smartphones grandes (iPhone 14 Pro Max, Galaxy S23, etc) */
@media (max-width: 480px) {
  

  .baselogo {
    width: 180px;
  }

  .logo1 {
    width: 32px;
    height: 45px;
    right: 145px;
  }

  .hamburger-button {
    width: 42px;
    height: 42px;
    margin-right: 12px;
    gap: 5px;
  }

  .hamburger-line {
    width: 35px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translateY(8px);
    width: 35px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(2) {
    transform: rotate(-45deg) translateY(-22px);
    width: 35px;
  }

  .mobile-menu {
    top: 56px;
    max-height: calc(100vh - 56px);
  }

  .mobile-nav-links li {
    padding: 12px 16px;
  }

  .mobile-nav-links li a {
    font-size: 14px;
  }

  .Buttondenuncia-mobile {
    width: calc(100% - 32px);
    margin: 16px;
    padding: 11px 16px;
    font-size: 14px;
    gap: 6px;
  }

  .Buttondenuncia-mobile .denuncia {
    width: 14px;
  }
}

/* Smartphones médios (iPhone 13/14, Galaxy S21, etc) */
@media (max-width: 390px) {

  .baselogo {
    width: 160px;
  }

  .logo1 {
    width: 30px;
    height: 42px;
    right: 130px;
  }

  .hamburger-button {
    width: 40px;
    height: 40px;
    margin-right: 10px;
  }

  .hamburger-line {
    width: 32px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translateY(7px);
    width: 32px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(2) {
    transform: rotate(-45deg) translateY(-20px);
    width: 32px;
  }

  .mobile-menu {
    top: 54px;
    max-height: calc(100vh - 54px);
  }

  .mobile-nav-links li {
    padding: 11px 14px;
  }

  .mobile-nav-links li a {
    font-size: 13px;
  }

  .Buttondenuncia-mobile {
    width: calc(100% - 28px);
    margin: 14px;
    padding: 10px 14px;
    font-size: 13px;
  }
}

/* Smartphones pequenos (iPhone SE, Galaxy A series, etc) */
@media (max-width: 360px) {

 
  .logo1 {
    width: 28px;
    height: 40px;
    right: 118px;
  }

  .hamburger-button {
    width: 38px;
    height: 38px;
    margin-right: 8px;
    gap: 4px;
  }

  .hamburger-line {
    width: 30px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translateY(6px);
    width: 30px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(2) {
    transform: rotate(-45deg) translateY(-18px);
    width: 30px;
  }

  .mobile-menu {
    top: 52px;
    max-height: calc(100vh - 52px);
  }

  .mobile-nav-links li {
    padding: 10px 12px;
  }

  .mobile-nav-links li a {
    font-size: 13px;
    line-height: 1.4;
  }

  .Buttondenuncia-mobile {
    width: calc(100% - 24px);
    margin: 12px;
    padding: 9px 12px;
    font-size: 13px;
    gap: 5px;
  }

  .Buttondenuncia-mobile .denuncia {
    width: 13px;
  }
}

/* Smartphones muito pequenos (iPhone S1st gen,E  etc) */
@media (max-width: 320px) {
 

  .baselogo {
    width: 130px;
    height: 100px;
  }

  .logo1 {
    width: 26px;
    height: 38px;
    right: 105px;
  }

  .hamburger-button {
    width: 36px;
    height: 36px;
    margin-right: 6px;
  }

  .hamburger-line {
    width: 28px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translateY(5px);
    width: 28px;
  }

  .hamburger-button.hamburger-active .hamburger-line:nth-child(2) {
    transform: rotate(-45deg) translateY(-16px);
    width: 28px;
  }

  .mobile-menu {
    top: 50px;
    max-height: calc(100vh - 50px);
  }

  .mobile-nav-links li {
    padding: 9px 10px;
  }

  .mobile-nav-links li a {
    font-size: 12px;
    line-height: 1.3;
  }

  .Buttondenuncia-mobile {
    width: calc(100% - 20px);
    margin: 10px;
    padding: 8px 10px;
    font-size: 12px;
    gap: 4px;
  }

  .Buttondenuncia-mobile .denuncia {
    width: 12px;
  }
}

/* Landscape mode para smartphones */
@media (max-height: 500px) and (orientation: landscape) {
  .mobile-menu {
    max-height: calc(100vh - 50px);
    overflow-y: auto;
  }

  .mobile-nav-links li {
    padding: 8px 15px;
  }

  .Buttondenuncia-mobile {
    margin: 10px 20px;
    padding: 8px 15px;
  }
}



</style>