<style>
 /* Fonts */
  @import url('https://fonts.googleapis.com/css2?family=Montserrat+Alternates&display=swap');

  .header {
  text-align: center;
  text-align: -webkit-center;
  text-align: -moz-center;
}
.mainApp {
  background-image: url("https://images.unsplash.com/photo-1454117096348-e4abbeba002c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  background-attachment: fixed;

}

.header-content {
  height: 10px;
  max-width: 800px;
}

.label-radio {
  color: rgba(0, 0, 0, 0.6);
  transform: translateY(-18px) translateX(-13%) scale(0.75);
}

.v-application {
  font-family: "Lato", sans-serif !important;
}

.v-input__slot {
  align-items: start !important;
}

input[type="number"] {
  -moz-appearance: textfield;
}

input::placeholder,
.v-file-input__text--placeholder {
  color: var(--v-placeholder-lighten2) !important;
  opacity: 1;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>

<template>
  <v-app>
    <Dialog />
    <v-main class="lighten-2 mainApp">
        <v-slide-x-transition leave-absolute><router-view /></v-slide-x-transition>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",
  components: {
    Dialog : () => import(/* webpackChunkName: "about" */ './components/Dialog.vue')
  },
};
</script>
