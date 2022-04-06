<template>
  <div class="container">
    <div class="header">
      <div class="header-content">
        <div class="col-4 primary d-inline-block rounded-tl-lg"></div>
        <div class="col-4 secondary d-inline-block"></div>
        <div class="col-4 accent d-inline-block rounded-tr-lg"></div>
      </div>
    </div>
    <div class="mx-auto my-auto" style="max-width: 800; background-color: #ddd">
      <h1>Pendataan Bansos</h1>
      <div>
        <b-form @submit="onSubmit" @reset="onReset" v-if="show">
          <b-form-group id="input-group-2" label="Nama" label-for="input-2">
            <b-form-input id="input-2" v-model="form.name" :rules="[(v) => !!v || 'Nama wajib Diisi']" placeholder="Masukan Nama Lengkap" required></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-2" label="Nama" label-for="input-2">
            <b-form-input id="input-2" v-model="form.name" :rules="[(v) => !!v || 'Nama wajib Diisi']" placeholder="Masukan Nama Lengkap" required></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-3" label="Food:" label-for="input-3">
            <b-form-select id="input-3" v-model="form.food" :options="foods" required></b-form-select>
          </b-form-group>

          <b-form-group id="input-group-4" v-slot="{ ariaDescribedby }">
            <b-form-checkbox-group v-model="form.checked" id="checkboxes-4" :aria-describedby="ariaDescribedby">
              <b-form-checkbox value="me">Check me out</b-form-checkbox>
              <b-form-checkbox value="that">Check that out</b-form-checkbox>
            </b-form-checkbox-group>
          </b-form-group>

          <b-button type="submit" variant="primary">Submit</b-button>
          <b-button type="reset" variant="danger">Reset</b-button>
        </b-form>
        <b-card class="mt-3" header="Form Data Result">
          <pre class="m-0">{{ form }}</pre>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: "",
        name: "",
        food: null,
        checked: [],
      },
      foods: [{ text: "Select One", value: null }, "Carrots", "Beans", "Tomatoes", "Corn"],
      show: true,
    };
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(event) {
      event.preventDefault();
      // Reset our form values
      this.form.email = "";
      this.form.name = "";
      this.form.food = null;
      this.form.checked = [];
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
  },
};
</script>
