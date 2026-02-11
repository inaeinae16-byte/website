<template>

  <div class="paragrafo">
    <h1>FISCALIZAMOS PARA PROTEGER, ORIENTAR <br> E FORTALECER O MERCADO MOÇAMBICANO</h1>
  </div>

</template>

<style scoped>
.paragrafo {
  display: flex;
  justify-content: center;

}

h1{
    display: flex;
    justify-content: center;
    font-family: black;
    color: var(--cor-verde);
    font-size: var(--f6);
    text-transform: capitalize;
    padding: 3rem;
 
}

@media (max-width: 720px) {

  .paragrafo {
    width: 100%;
    height: 200px;
    margin-bottom: 50px;
    margin-top: 40px;
  }

  h1{
    font-size:var(--f5);
    padding: 0 0 2px 2px ;
    text-align: center;
  }
}
</style>