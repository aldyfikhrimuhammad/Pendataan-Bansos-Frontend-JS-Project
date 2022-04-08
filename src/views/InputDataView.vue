<template>
  <div class="container" style="border: 1px solid red; margin: 20px auto; padding: 25px">
    <div class="rounded dataSection">
      <h1 class="m-3">Pendataan Bansos</h1>
      <div>
        <form class="needs-validation" novalidate style="padding: 20px 50px">
          <!-- Form Input Nama Lengkap -->
          <div class="mb-3">
            <label class="form-label">Nama</label>
            <input type="text" class="form-control" name="nama" v-model="nama" :rules="[(v) => !!v || 'Nama wajib Diisi']" label="Nama" placeholder="Masukan Nama Lengkap" persistent-placeholder required />
          </div>

          <!-- Form Input NIK -->
          <div class="mb-3">
            <label class="form-label">NIK</label>
            <input
              type="number"
              class="form-control"
              v-model="nik"
              name="nik"
              :counter="16"
              @keypress="cekNumber"
              :rules="[(v) => !!v || 'NIK wajib diisi', rules.nik]"
              label="NIK"
              placeholder="Contoh : 3211221902xxxxxx"
              persistent-placeholder
              required
            />
          </div>

          <!-- Form Input Nomor KK -->
          <div class="mb-3">
            <label class="form-label">Nomor Kartu Keluarga</label>
            <input
              type="number"
              class="form-control"
              v-model="noKK"
              name="kk"
              :counter="16"
              @keypress="cekNumber"
              :rules="[(v) => !!v || 'Nomor Kartu Keluarga wajib diisi', rules.kk]"
              label="Nomor Kartu Keluarga"
              placeholder="Contoh : 3211220114xxxxxx"
              persistent-placeholder
              required
            />
          </div>

          <div class="d-flex justify-content-left">
            <!-- Form Input Umur -->
            <div class="mb-3">
              <label class="form-label">Umur</label>
              <input type="number" class="form-control" v-model="umur" rules="[(v) => !!v || 'Umur wajib diisi', rules.umur]" label="Umur" placeholder="Minimal 25 Tahun" persistent-placeholder required />
            </div>
            <!-- Form Input Jenis Kelamin -->
            <div class="mb-3 ml-5">
              <label class="form-label mr-3">Jenis Kelamin : </label>
              <div class="form-check form-check-inline d-block">
                <table style="text-align: left">
                  <tr>
                    <td>
                      <input class="form-check-input" type="radio" name="jenisKelamin" id="jenisKelamin1" value="Laki-laki" v-model="jenisKelamin" :rules="[(v) => !!v || 'Jenis Kelamin wajib diisi']" required />
                      <label class="form-check-label" value="Laki-laki">Laki-laki</label>
                    </td>
                  </tr>
                  <tr>
                    <td>
                      <div class="form-check form-check-inline">
                        <input class="form-check-input" type="radio" name="jenisKelamin" id="jenisKelamin2" value="Perempuan" v-model="jenisKelamin" :rules="[(v) => !!v || 'Jenis Kelamin wajib diisi']" required />
                        <label class="form-check-label" value="Perempuan">Perempuan</label>
                      </div>
                    </td>
                  </tr>
                </table>
              </div>
            </div>
          </div>

          <!-- Form Input Alamat -->
          <div class="mb-3">
            <label class="form-label">Alamat</label>
            <textarea class="form-control" v-model="alamat" name="alamat" :rules="[(v) => !!v || 'Alamat wajib diisi', rules.alamat]" placeholder="Masukan Alamat Lengkap" persistent-placeholder rows="1" no-resize auto-grow></textarea>
          </div>

          <div class="d-flex">
            <!-- Form Input RT -->
            <div class="mb-3 mr-1">
              <label class="form-label">RT</label>
              <input type="number" class="form-control" v-model="RT" @keypress="cekNumber" :rules="[(v) => !!v || 'RT wajib Diisi']" label="RT" placeholder="Contoh: 001" persistent-placeholder required />
            </div>
            <!-- Form Input RW -->
            <div class="mb-3 ml-1">
              <label class="form-label">RW</label>
              <input type="number" class="form-control" v-model="RW" @keypress="cekNumber" :rules="[(v) => !!v || 'RW wajib Diisi']" label="RW" placeholder="Contoh: 004" persistent-placeholder required />
            </div>
          </div>

          <div class="d-flex">
            <!-- Form Input Penghasilan Sebelum Pandemi -->
            <div class="mb-3 mr-1">
              <label class="form-label">Penghasilan Sebelum Pandemi</label>
              <input
                type="number"
                class="form-control"
                v-model="PengSebelumPandemi"
                @keypress="cekNumber"
                :rules="[(v) => !!v || 'Penghasilan Sebelum Pandemi wajib Diisi']"
                label="Penghasilan Sebelum Pandemi"
                prefix="Rp."
                placeholder="0-,"
                persistent-placeholder
                required
              />
            </div>
            <!-- Form Input Penghasilan Setelah Pandemi -->
            <div class="mb-3 ml-1">
              <label class="form-label">Penghasilan Setelah Pandemi</label>
              <input
                type="number"
                class="form-control"
                v-model="PengSetelahPandemi"
                @keypress="cekNumber"
                :rules="[(v) => !!v || 'Penghasilan Setelah Pandemi wajib Diisi']"
                label="Penghasilan Setelah Pandemi"
                prefix="Rp."
                placeholder="0-,"
                persistent-placeholder
                required
              />
            </div>
          </div>

          <!-- Form Input Alasan Menerima Bantuan Use Select -->
          <div class="mb-3">
            <label class="form-label">Alasan Membutuhkan Bantuan</label>
            <b-form-select
              v-model="alasanTerpilih"
              :options="alasanList"
              :rules="[(v) => !!v || 'Alasan wajib diisi']"
              label="Alasan membutuhkan bantuan"
              placeholder="Pilih salah satu"
              :menu-props="{ overflowX: true }"
              attach
              persistent-placeholder
              auto
              required
            ></b-form-select>

            <div class="mb-3">
              <input type="text" class="form-control" v-model="alasanLainnya" v-if="alasanTerpilih == 'Lainnya'" :rules="[(v) => !!v || 'Alasan wajib diisi']" placeholder="Tulis alasan disini" persistent-placeholder required />
            </div>
          </div>

          <!-- Form Input Foto KTP -->
          <div class="mb-3 d-flex">
            <label class="form-label mt-2" style="width: 101px; text-align: left">Foto KTP</label>
            <input
              type="file"
              class="form-control uploadButton"
              show-size
              ref="ktp"
              @change="cekKTP"
              prepend-icon="mdi-cloud-upload"
              :rules="[(v) => !!v || 'Foto KTP wajib diisi', rules.photoSize, rules.photoType]"
              accept="image/png, image/jpeg, image/jpeg, image/bmp"
              placeholder="Pilih File"
              persistent-placeholder
            />
          </div>

          <!-- Form Input Foto KK -->
          <div class="mb-3 d-flex">
            <label class="form-label mt-2" style="width: 100px; text-align: left">Foto KK</label>
            <input
              type="file"
              class="form-control uploadButton"
              show-size
              ref="kk"
              @change="cekKK"
              prepend-icon="mdi-cloud-upload"
              :rules="[(v) => !!v || 'Foto KK wajib diisi', rules.photoSize, rules.photoType]"
              accept="image/png, image/jpeg, image/jpeg, image/bmp"
              placeholder="Pilih File"
              persistent-placeholder
            />
          </div>
          <div>
          <div class="text-caption text--secondary font-weight-light font-italic d-flex mb-2" v-for="(message, index) in messagesFoto" :key="`message-${index}`">
            <div><span v-for="(n, i) in index + 1" :key="i + 1">*</span></div>
            <div>
              <span>&nbsp;{{ message }}</span>
            </div>
          </div>
        </div>

          <!-- Form Input Checkbox -->
          <div class="mb-3">
            <div class="form-check">
              <input class="form-check-input" type="checkbox" v-model="check" id="agreement" :rules="[(v) => !!v || 'Harap setujui untuk melanjutkan!']" :ripple="false" required/>
              <label class="form-check-label"> Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut. </label>
            </div>
          </div>

          <div v-show="!valid" class="error--text my-2 text-subtitle"><span>Mohon Pastikan Data telah terisi seluruhnya!</span></div>

          <!-- Create Button Submit -->
          <div class="text-center">
          <button :disabled="!valid" :loading="loadingButton" elevation="3" class="mr-4 rounded submitButton" type="submit">Simpan</button>
        </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style>
form {
  max-width: 500px;
  margin: 0 auto;
}
h1 {
  text-align: center;
  font-size: 3rem;
  font-weight: bolder;
  line-height: 1.2;
  margin-bottom: 3rem;
  background: black;
  text-shadow: 11px 8px 16px rgba(0, 0, 0, 0.4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.form-label {
  font-weight: 400;
}
.form-control {
  border: 1px solid green;
}
.dataSection {
    background-image: url("/src/assets/background.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  background-attachment: fixed;
  width: 100%;
  height: 100%;
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
</style>

<script>
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
