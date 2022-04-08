<template>
  <v-container style="margin: 20px auto; padding: 10px auto">
    <v-card class="rounded mainCard" max-width="800" outlined elevation="3">
      <h1 class="text-center text-headline mb-6">Formulir Data Bansos</h1>
      <v-form ref="form" v-model="valid" @submit.prevent="submit" lazy-validation>
        <!-- Form Input Nama Lengkap -->
        <v-text-field class="mb-4" v-model="nama" :rules="[(v) => !!v || 'Nama wajib Diisi']" label="Nama" placeholder="Masukan Nama Lengkap" persistent-placeholder required></v-text-field>

        <!-- Form Input NIK -->
        <v-text-field
          class="mb-4"
          v-model="nik"
          name="nik"
          :counter="16"
          @keypress="cekNumber"
          :rules="[(v) => !!v || 'NIK wajib diisi', rules.nik]"
          label="NIK"
          type="number"
          placeholder="Contoh : 3211221902xxxxxx"
          persistent-placeholder
          required
        ></v-text-field>

        <!-- Form Input Nomor KK -->
        <v-text-field
          class="mb-4"
          v-model="noKK"
          name="kk"
          :counter="16"
          @keypress="cekNumber"
          :rules="[(v) => !!v || 'Nomor Kartu Keluarga wajib diisi', rules.kk]"
          label="Nomor Kartu Keluarga"
          type="number"
          placeholder="Contoh : 3211220114xxxxxx"
          persistent-placeholder
          required
        ></v-text-field>

        <div class="row mb-4">
          <!-- Form Input Umur -->
          <v-text-field v-model="umur" class="col-12 col-sm-6" :rules="[(v) => !!v || 'Umur wajib diisi', rules.umur]" label="Umur" type="number" placeholder="Minimal 25 Tahun" persistent-placeholder required></v-text-field>
          <!-- Form Radio Jenis Kelamin -->
          <div class="col-12 col-sm-6">
            <div class="label-radio"><span>Jenis Kelamin</span></div>
            <v-radio-group v-model="jenisKelamin" mandatory row hide-details class="ma-0 ma-mb-0 mt-n3">
              <v-radio label="Laki-laki" value="Laki-laki"></v-radio>
              <v-radio label="Perempuan" value="Perempuan"></v-radio>
            </v-radio-group>
          </div>
        </div>

        <!-- Form Input Alamat Lengkap -->
        <v-textarea v-model="alamat" class="mb-4" :rules="[(v) => !!v || 'Alamat wajib diisi', rules.alamat]" label="Alamat" placeholder="Masukan Alamat Lengkap" persistent-placeholder rows="1" no-resize auto-grow></v-textarea>

        <!-- Form Input RT/RW -->
        <div class="row mb-4 ">
          <!--- Form Input RT -->
          <v-text-field v-model="RT" @keypress="cekNumber" class="col-6" :rules="[(v) => !!v || 'RT wajib Diisi']" label="RT" type="number" placeholder="Masukan RT (Contoh: 001)" persistent-placeholder required></v-text-field>
          <!-- Form Input RW -->
          <v-text-field v-model="RW" @keypress="cekNumber" class="col-6" :rules="[(v) => !!v || 'RW wajib Diisi']" label="RW" type="number" placeholder="Masukan RW (Contoh: 004)" persistent-placeholder required></v-text-field>
        </div>

        <!-- Form Input Penghasilan -->
        <div class="row mb-4 ">
          <!-- Form Input Penghasilan - Sebelum -->
          <v-text-field
            v-model="PengSebelumPandemi"
            @keypress="cekNumber"
            class="col-12 col-sm-6 mb-4 mb-sm-0"
            :rules="[(v) => !!v || 'Penghasilan Sebelum Pandemi wajib Diisi']"
            label="Penghasilan Sebelum Pandemi"
            type="number"
            prefix="Rp."
            placeholder="0-,"
            persistent-placeholder
            required
          ></v-text-field>
          <!-- Form Input Penghasilan - Sesudah -->
          <v-text-field
            v-model="PengSetelahPandemi"
            @keypress="cekNumber"
            class="col-12 col-sm-6"
            :rules="[(v) => !!v || 'Penghasilan Setelah Pandemi wajib Diisi']"
            label="Penghasilan Setelah Pandemi"
            type="number"
            prefix="Rp."
            placeholder="0-,"
            persistent-placeholder
            required
          ></v-text-field>
        </div>

        <!-- Form Input Alasan -->
        <div class="mb-4">
          <v-select
            v-model="alasanTerpilih"
            :items="alasanList"
            :rules="[(v) => !!v || 'Alasan wajib diisi']"
            label="Alasan membutuhkan bantuan"
            placeholder="Pilih salah satu"
            :menu-props="{ overflowX: true }"
            attach
            persistent-placeholder
            auto
            required
          ></v-select>

          <v-scale-transition>
            <v-text-field v-model="alasanLainnya" v-if="alasanTerpilih == 'Lainnya'" class="mt-n3" :rules="[(v) => !!v || 'Alasan wajib diisi']" placeholder="Tulis alasan disini" persistent-placeholder required></v-text-field>
          </v-scale-transition>
        </div>
        <!-- Form Input Foto KK -->
        <div>
          <table>
            <tr>
              <td><label>Foto KTP</label></td>
              <td>
                <v-btn class="uploadButton rounded">
                  <v-file-input
                    show-size
                    ref="ktp"
                    @change="cekKTP"
                    v-model="fotoKTP"
                    prepend-icon="mdi-cloud-upload"
                    :rules="[(v) => !!v || 'Foto KTP wajib diisi', rules.photoSize, rules.photoType]"
                    accept="image/png, image/jpeg, image/jpeg, image/bmp"
                    placeholder="Pilih File"
                    persistent-placeholder
                  >
                  </v-file-input>
                </v-btn>
              </td>
            </tr>
            <tr>
              <td><label>Foto KK</label></td>
              <td>
                <v-btn class="uploadButton rounded">
                  <v-file-input
                    show-size
                    ref="kk"
                    @change="cekKK"
                    v-model="fotoKK"
                    prepend-icon="mdi-cloud-upload"
                    :rules="[(v) => !!v || 'Foto KK wajib diisi', rules.photoSize, rules.photoType]"
                    accept="image/png, image/jpeg, image/jpeg, image/bmp"
                    placeholder="Pilih File"
                    persistent-placeholder
                  >
                  </v-file-input>
                </v-btn>
              </td>
            </tr>
          </table>
        </div>
        <div>
          <div class="text-caption text--secondary font-weight-light font-italic d-flex" v-for="(message, index) in messagesFoto" :key="`message-${index}`">
            <div><span v-for="(n, i) in index + 1" :key="i + 1">*</span></div>
            <div>
              <span>&nbsp;{{ message }}</span>
            </div>
          </div>
        </div>

        <!-- Form Input Checkbox -->
        <v-checkbox v-model="check" class="mb-6" id="agreement" :rules="[(v) => !!v || 'Harap setujui untuk melanjutkan!']" :ripple="false" required>
          <template v-slot:label>Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.</template>
        </v-checkbox>

        <div v-show="!valid" class="error--text my-2 text-subtitle"><span>Mohon Pastikan Data telah terisi seluruhnya!</span></div>
        <div class="text-center text-md-left">
          <v-btn :disabled="!valid" :block="$vuetify.breakpoint.mobile" :loading="loadingButton" elevation="3" color="success" class="mr-4 rounded px-16 py-6 px-md-14 submitButton" type="submit">Simpan</v-btn>
        </div>
      </v-form>
    </v-card>
  </v-container>
</template>

<style>
h1 {
  font-size: 3rem;
  font-weight: bolder;
  line-height: 1.2;
  margin-bottom: 3rem;
  background: black;
  text-shadow: 11px 8px 16px rgba(0, 0, 0, 0.4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.uploadButton {
  margin: 5px 20px 20px 10px;
  background-color: #ffffff;
  color: #000000;
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.1);
}
.uploadButton:hover {
  background-color: #fafafa;
  color: #000000;
  transform: translateX(3px);
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.2);
}
.submitButton {
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.2);
}
.submitButton:hover {
  background-color: #fafafa;
  color: #000000;
  transform: translateY(3px);
  box-shadow: 10px 10px 10px rgba(0, 0, 0, 0.2);
}
.mainCard {
  box-shadow: 15px 14px 35px 14px rgba(0, 0, 0, 0.60);
  -webkit-box-shadow: 15px 15px 35px 15px rgba(0, 0, 0, 0.60);
  -moz-box-shadow: 15px 15px 35px 15px rgba(0, 0, 0, 0.60);
  margin: 25px auto;
  padding: 50px;
}
</style>

<script>
import { mapActions } from "vuex";

export default {
  data: () => ({
    valid: true,
    loadingButton: false,
    nama: "",
    nik: "",
    noKK: "",
    fotoKTP: null,
    fotoKTPPreview: "https://via.placeholder.com/150x150?text=KTP",
    fotoKKPreview: "https://via.placeholder.com/150x150?text=KK",
    fotoKK: null,
    umur: "",
    alamat: "",
    jenisKelamin: "",
    RT: "",
    RW: "",
    PengSebelumPandemi: "",
    PengSetelahPandemi: "",
    alasanTerpilih: null,
    alasanLainnya: "",
    alasanList: ["Kehilangan Pekerjaan", "Kepala keluarga terdampak atau korban Covid", "Tergolong fakir/miskin semenjak sebelum Covid", "Lainnya"],
    check: false,
    messagesFoto: ["Foto tidak boleh lebih dari 2MB", "Format file PNG/JPG/JPEG/BMP"],
    rules: {
      photoSize: (v) => !v || v.size <= 2000000 || "Ukuran file terlalu besar",
      photoType: (v) => !v || ["image/png", "image/jpeg", "image/jpeg", "image/bmp"].indexOf(v.type) >= 0 || "Format file salah",
      umur: (v) => (v && v >= 25) || "Umur harus 25 atau keatas",
      nik: (v) => (v && v.length == 16) || "NIK harus berjumlah 16 digit",
      kk: (v) => (v && v.length == 16) || "Nomor KK harus berjumlah 16 digit",
      alamat: (v) => (v && v.length <= 255) || "Alamat tidak boleh lebih dari 255 karakter",
    },
  }),
  computed: {
    statusKTP() {
      return this.$refs.ktp;
    },
    statusKK() {
      return this.$refs.kk;
    },
    inputedData() {
      return {
        nama: this.nama,
        nik: this.nik,
        noKK: this.noKK,
        fotoKTP: this.fotoKTP,
        fotoKK: this.fotoKK,
        umur: this.umur,
        alamat: this.alamat,
        jenisKelamin: this.jenisKelamin,
        RT: this.RT,
        RW: this.RW,
        PengSebelumPandemi: this.PengSebelumPandemi,
        PengSetelahPandemi: this.PengSetelahPandemi,
        alasan: this.alasan,
      };
    },
    alasan() {
      if (this.alasanTerpilih && this.alasanTerpilih == "Lainnya") {
        return this.alasanLainnya;
      }

      return this.alasanTerpilih;
    },
  },
  methods: {
    ...mapActions({
      setDialogStatus: "dialog/setStatus",
    }),

    sleep(ms) {
      return new Promise((resolve) => setTimeout(resolve, ms));
    },

    randomNumber(min, max) {
      return Math.random() * (max - min) + min;
    },

    async submit() {
      if (this.$refs.form.validate()) {
        let time = Math.floor(this.randomNumber(1400, 1600));
        console.log({
          responseTime: time,
          data: this.inputedData,
        });
        this.loadingButton = true;
        await this.sleep(time);
        if (time >= 1500) {
          this.loadingButton = false;
          this.setDialogStatus(true);
        } else {
          this.loadingButton = false;
          this.$router.push({
            name: "Info",
            params: {
              savedForm: true,
            },
          });
        }
      }
    },

    cekKTP() {
      if (this.statusKTP.validate()) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.fotoKTPPreview = e.target.result;
        };
        reader.readAsDataURL(this.fotoKTP);
      } else {
        this.fotoKTPPreview = "https://via.placeholder.com/150x150?text=KK";
      }
    },

    cekKK() {
      if (this.statusKK.validate()) {
        const reader = new FileReader();

        reader.onload = (e) => {
          this.fotoKKPreview = e.target.result;
        };
        reader.readAsDataURL(this.fotoKK);
      } else {
        this.fotoKKPreview = "https://via.placeholder.com/150x150?text=KK";
      }
    },

    cekNumber(event) {
      if ((event.which != 8 && event.which != 0 && event.which < 48) || event.which > 57) {
        event.preventDefault();
      }

      if (event.target.name == "nik" || event.target.name == "kk") {
        if (event.target.value.length >= 16) {
          event.preventDefault();
        }
      }
    },
  },
  beforeMount() {
    document.title = this.$route.meta.title;
  },
};
</script>
