<template>
  <div class="home">
    <div>
    <img src="/data-bansos/src/assets/LogoJabar.png" alt="Logo Provinsi Jawa Barat" width="250" height="250">
  <b-jumbotron lead="Selamat Datang!" text-variant="dark" class="jumbotron">
    <h3>Lorem ipsum dolor sit amet</h3>
      <hr class="my-4">
    <p>lorem ipsum dolor sit amet</p>
    <router-link to="/inputData" class="mr-2 ml-3">
      <b-button pill variant="success" class="buttonHome">Isi Formulir</b-button>
    </router-link>
  </b-jumbotron>
</div>
  </div>
</template>

<style>
.jumbotron {
  padding: 2rem 1rem 12rem;
  background-color: #fff !important;
}
.buttonHome:hover {
  transform: translate(5px, 5px);
  transition: 0.2s;
  box-shadow: 0px 0px 5px #42b983;
}
</style>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Home',
  props: {
    msg: String
  }
}
</script>
