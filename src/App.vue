<template>
  <div id="app">
    <!-- Navbar -->
    <div>
      <b-navbar toggleable="lg" type="light" variant="light">
        <router-link to="/">
              <b-navbar-brand>
                <h2 class="title">Data Bansos Jabar</h2>
              </b-navbar-brand>
            </router-link>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="ml-auto">
            <b-navbar-nav>
              <router-link to="/" class="mr-2 ml-3">
              <div class="d-flex justify-content-center">
                <b-icon icon="house-door-fill" class="my-1 mx-2"></b-icon>
                <h5><strong>Beranda</strong></h5>
              </div>
              </router-link>
              <router-link to="/inputData" class="mr-2 ml-3">
                <div class="d-flex justify-content-center">
                  <b-icon icon="person-lines-fill" class="my-1 mx-2"></b-icon>
                  <h5><strong>Input Data</strong></h5>
                </div>
              </router-link>
            </b-navbar-nav>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>

    <!-- Router View -->
    <router-view />

    <!-- Footer -->
    <footer class="bg-light text-center text-black">
      <div class="text-center p-3">
        © 2022 Copyright:
        <a class="text-dark" href="https://www.linkedin.com/in/aldyfikhrimuhammad/">Aldy Fikhri Muhammad</a>
      </div>
    </footer>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}
nav a {
  color: #42b983 ;
}
nav a:hover {
  color: #42b983 ;
}
nav a:active {
  color: #42b983 ;
}
.title {
  font-size: 1.5rem;
  font-weight: bolder;
  color: #42b983;
  text-shadow: 4px 4px 4px #ddd;
}
button:hover {
  box-shadow: 0px 0px 5px #42b983;
}

</style>
