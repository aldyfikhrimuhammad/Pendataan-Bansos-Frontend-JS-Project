<template>
  <div class="home">
    <div>
  <b-jumbotron text-variant="dark" class="jumbotron">
  <img src="data-bansos/src/assets/LogoJabar.png" alt="Logo Provinsi Jawa Barat" width="250" height="250">
  <h5 class="d-flex ml-4">Selamat Datang Di</h5>
  <h1 class="display-5 m-2">Sistem Pendataan Bantuan Sosial Provinsi Jawa Barat</h1>
      <hr class="my-4">
    <p class="px-5 mx-5 mb-2">Guna memastikan bantuan tersalurkan kepada orang yang tepat dan data yang masuk bersifat valid, dibutuhkan verifikasi sejumlah data yang wajib dilaporkan.</p>
    <router-link to="/inputData" class="mr-2 ml-3">
      <b-button pill variant="success" class="buttonHome">Isi Formulir</b-button>
    </router-link>
  </b-jumbotron>
</div>
  </div>
</template>

<style>
.jumbotron {
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("/src/assets/background.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  background-attachment: fixed;
  height: 100vh;
  width: 100%;
}
.buttonHome:hover {
  transform: translate(5px, 5px);
  transition: 0.2s;
  box-shadow: 0px 0px 5px #42b983;
}
h1 {
  font-weight: bolder;
}
p {
  font-size: 1.5rem;
  margin: 10px auto;
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
