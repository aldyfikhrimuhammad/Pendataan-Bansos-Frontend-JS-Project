<template>
  <div class="container">
    <div class="rounded dataSection">
      <h1 class="m-3">Pendataan Bansos</h1>
      <div>
        <form class="needs-validation" novalidate style="border: 1px solid blue; padding: 20px 50px;">
          <!-- Form Input Nama Lengkap -->
          <div class="mb-3">
            <label class="form-label">Nama</label>
            <input type="text" class="form-control" v-model="nama" name="nama" :rules="[v => !!v || 'Nama wajib Diisi']" placeholder="Masukan Nama Lengkap" persistent-placeholder required />
          </div>

          <!-- Form Input NIK -->
          <div class="mb-3">
            <label class="form-label">NIK</label>
            <input type="text" class="form-control" v-model="nik" name="nik" :counter="16" @keypress="cekNumber" :rules="[v => !!v || 'NIK wajib diisi', rules.nik]" color="accent" placeholder="Contoh : 32112xxxxxxxxxxx" persistent-placeholder required />
          </div>

          <!-- Form Input Nomor KK -->
          <div class="mb-3">
            <label class="form-label">Nomor Kartu Keluarga</label>
            <input type="text" class="form-control" v-model="noKK" name="kk" :counter="16" @keypress="cekNumber" :rules="[v => !!v || 'Nomor Kartu Keluarga wajib diisi', rules.kk]" placeholder="Contoh : 32113xxxxxxxxxxx" persistent-placeholder required />
          </div>

          <!-- Form Input Umur -->
          <div class="mb-3">
            <label class="form-label">Umur</label>
            <input type="text" class="form-control" v-model="umur" :rules="[v => !!v || 'Umur wajib diisi', rules.umur]" @keypress="cekNumber" placeholder="Minimal 25 Tahun" persistent-placeholder required />
          </div>

          <!-- Form Input Jenis Kelamin -->
          <div class="mb-3">
            <label class="form-label mr-3">Jenis Kelamin : </label>
            <div class="form-check form-check-inline">
              <input class="form-check-input" type="radio" name="jenisKelamin" id="jenisKelamin1" value="Laki-laki" v-model="jenisKelamin" :rules="[v => !!v || 'Jenis Kelamin wajib diisi']" required />
              <label class="form-check-label" for="jenisKelamin1">Laki-laki</label>
            </div>
            <div class="form-check form-check-inline">
              <input class="form-check-input" type="radio" name="jenisKelamin" id="jenisKelamin2" value="Perempuan" v-model="jenisKelamin" :rules="[v => !!v || 'Jenis Kelamin wajib diisi']" required />
              <label class="form-check-label" for="jenisKelamin2">Perempuan</label>
            </div>
          </div>

          <!-- Form Input Alamat -->
          <div class="mb-3">
            <label class="form-label">Alamat</label>
            <textarea class="form-control" v-model="alamat" name="alamat" :rules="[v => !!v || 'Alamat wajib diisi']" placeholder="Masukan Alamat Lengkap" persistent-placeholder required></textarea>
          </div>

          <!-- Form Input RT -->
          <div class="mb-3">
            <label class="form-label">RT</label>
            <input type="text" class="form-control" v-model="rt" :rules="[v => !!v || 'RT wajib diisi', rules.rt]" @keypress="cekNumber" placeholder="Contoh : 001" persistent-placeholder required />
          </div>

          <!-- Form Input RW -->
          <div class="mb-3">
            <label class="form-label">RW</label>
            <input type="text" class="form-control" v-model="rw" :rules="[v => !!v || 'RW wajib diisi', rules.rw]" @keypress="cekNumber" placeholder="Contoh : 004" persistent-placeholder required />
          </div>

          <!-- Form Input Penghasilan Sebelum Pandemi -->
          <div class="mb-3">
            <label class="form-label">Penghasilan Sebelum Pandemi</label>
            <input type="text" class="form-control" v-model="penghasilanSebelumPandemi" :rules="[v => !!v || 'Penghasilan Sebelum Pandemi wajib diisi', rules.penghasilanSebelumPandemi]" @keypress="cekNumber" placeholder="Contoh : Rp. 1.000.000" persistent-placeholder required />
          </div>

          <!-- Form Input Penghasilan Setelah Pandemi -->
          <div class="mb-3">
            <label class="form-label">Penghasilan Setelah Pandemi</label>
            <input type="text" class="form-control" v-model="penghasilanSetelahPandemi" :rules="[v => !!v || 'Penghasilan Setelah Pandemi wajib diisi', rules.penghasilanSetelahPandemi]" @keypress="cekNumber" placeholder="Contoh : Rp. 1.000.000" persistent-placeholder required />
          </div>

          <!-- Form Input Alasan Menerima Bantuan Use Select -->
          <div class="mb-3">
            <label class="form-label">Alasan Menerima Bantuan</label>
            <select class="form-control" v-model="alasanTerpilih"
            :items="alasanList"
            :rules="[(v) => !!v || 'Alasan wajib diisi']"
            label="Alasan membutuhkan bantuan"
            placeholder="Pilih salah satu"
            :menu-props="{ overflowX: true }"
            attach
            persistent-placeholder
            auto
            required>
            </select>

            <div class="invalid-feedback">
              Alasan wajib diisi
            </div>
          </div>

          <!-- Form Input Foto KTP -->
          <div class="mb-3 d-flex">
            <label class="form-label mt-2" style="width: 101px; text-align: left;">Foto KTP</label>
            <input type="file" class="form-control"  name="fotoKTP" :rules="[v => !!v || 'Foto KTP wajib diisi']" placeholder="Masukan Foto KTP" persistent-placeholder required />
          </div>

          <!-- Form Input Foto KK -->
          <div class="mb-3 d-flex">
            <label class="form-label mt-2" style="width: 100px; text-align: left">Foto KK</label>
            <input type="file" class="form-control" name="fotoKK" :rules="[v => !!v || 'Foto Kartu Keluarga wajib diisi']" placeholder="Masukan Foto Kartu Keluarga" persistent-placeholder required />
          </div>

          <!-- Form Input Checkbox -->
          <div class="mb-3">
            <div class="form-check">
              <input class="form-check-input" type="checkbox" v-model="check"  :rules="[(v) => !!v || 'Harap setujui untuk melanjutkan!']" :ripple="false" required />
              <label class="form-check-label">
                Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.
              </label>
            </div>
          </div>

          <!-- Create Button Submit -->
          <button class="btn btn-primary" type="submit">Submit</button>



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
  font-weight: bolder;
  text-shadow: 2px 2px 4px #000000;
  color: #fff;
}
.form-label {
  font-weight: 400;
  color: #fff;
}
.form-control {
  border: 1px solid green;
}
.dataSection {
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("/src/assets/background.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  background-attachment: fixed;
  width: 100%;
  height: 100%;
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
    onSubmit(event) {
      event.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(event) {
      event.preventDefault();
      // Reset our form values
      this.nama = "";
      this.food = null;
      this.checked = [];
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
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
};
</script>
