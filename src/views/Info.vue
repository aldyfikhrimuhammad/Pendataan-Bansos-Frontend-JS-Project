<template>
  <v-container class="text-center" v-if="this.$route.params.savedForm">
    <v-card class="mx-auto px-7 py-10 rounded-b-lg rounded-t-0" max-width="800" outlined elevation="3">
      <h1 class="text-headline success--text">Berhasil!</h1>
      <v-divider class="my-2"></v-divider>
      <p>Data berhasil disimpan.</p>
      <v-btn rounded color="success" class="rounded px-16 py-6 tambahButton" to="/">Tambah Data Baru</v-btn>
    </v-card>
  </v-container>
</template>

<style>
.tambahButton {
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.2);
}
.tambahButton:hover {
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.4);
  background-color: #fafafa;
  color: #000000;
  transform: translateY(3px);
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.2);
}
</style>

<script>
export default {
  beforeCreate() {
    if (!this.$route.params.savedForm) {
      document.title = this.$route.meta.title;
      this.$router.push("/");
    } else {
      document.title = "Berhasil disimpan";
    }
  },
};
</script>
