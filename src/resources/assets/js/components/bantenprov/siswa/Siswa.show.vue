<template>
  <div class="card">
    <div class="card-header">
      <i class="fa fa-table" aria-hidden="true"></i> siswa : {{ model.nama_siswa }}

      <ul class="nav nav-pills card-header-pills pull-right">
        <li class="nav-item">
          <button class="btn btn-primary btn-sm" role="button" @click="back">
            <i class="fa fa-arrow-left" aria-hidden="true"></i>
          </button>
        </li>
      </ul>
    </div>

    <div class="card-body">
      <vue-form class="form-horizontal form-validation" :state="state" @submit.prevent="onSubmit">
        <div class="card-body">
          <dl class="row">
              <dt class="col-2">Nomor UN :</dt>
              <dd class="col-10">{{ model.nomor_un }}</dd>

              <dt class="col-2">NIK :</dt>
              <dd class="col-10">{{ model.nik }}</dd>

              <dt class="col-2">Nama Siswa :</dt>
              <dd class="col-10">{{ model.nama_siswa }}</dd>

              <dt class="col-2">Nomor KK :</dt>
              <dd class="col-10">{{ model.no_kk }}</dd>

              <dt class="col-2">Alamat KK :</dt>
              <dd class="col-10">{{ model.alamat_kk }}</dd>

              <dt class="col-2">Provinsi :</dt>
              <dd class="col-10">{{ model.province_id }}</dd>

              <dt class="col-2">Kota :</dt>
              <dd class="col-10">{{ model.city_id }}</dd>

              <dt class="col-2">Kecamatan :</dt>
              <dd class="col-10">{{ model.district_id }}</dd>

              <dt class="col-2">Desa :</dt>
              <dd class="col-10">{{ model.village_id }}</dd>

              <dt class="col-2">Tempat Lahir :</dt>
              <dd class="col-10">{{ model.tempat_lahir }}</dd>

              <dt class="col-2">Tanggal Lahir :</dt>
              <dd class="col-10">{{ model.tgl_lahir }}</dd>

              <dt class="col-2">Jenis Kelamin :</dt>
              <dd class="col-10">{{ model.jenis_kelamin }}</dd>

              <dt class="col-2">Agama :</dt>
              <dd class="col-10">{{ model.agama }}</dd>

              <dt class="col-2">NISN :</dt>
              <dd class="col-10">{{ model.nisn }}</dd>

              <dt class="col-2">Tahun Lulus :</dt>
              <dd class="col-10">{{ model.tahun_lulus }}</dd>

              <dt class="col-2">Sekolah Tujuan:</dt>
              <dd class="col-10">{{ model.sekolah.label }}</dd>
          </dl>
        </div>

      </vue-form>
    </div>
       <div class="card-footer text-muted">
        <div class="row">
          <div class="col-md">
            <b>Username :</b> {{ model.user.name }}
          </div>
          <div class="col-md">
            <div class="col-md text-right">Dibuat : {{ model.created_at }}</div>
            <div class="col-md text-right">Diperbaiki : {{ model.updated_at }}</div>
          </div>
        </div>
      </div>
</div>
</template>

<script>
export default {
  mounted() {
    axios.get('api/siswa/' + this.$route.params.id)
      .then(response => {
        if (response.data.status == true) {
          this.model.user           = response.data.siswa.user;
          this.model.nomor_un       = response.data.siswa.nomor_un;
          this.model.nik            = response.data.siswa.nik;
          this.model.nama_siswa     = response.data.siswa.nama_siswa;
          this.model.no_kk          = response.data.siswa.no_kk;
          this.model.alamat_kk      = response.data.siswa.alamat_kk;
          this.model.province_id    = response.data.siswa.province_id;
          this.model.city_id        = response.data.siswa.city_id;
          this.model.district_id    = response.data.siswa.district_id;
          this.model.village_id     = response.data.siswa.village_id;
          this.model.tempat_lahir   = response.data.siswa.tempat_lahir;
          this.model.tgl_lahir      = response.data.siswa.tgl_lahir;
          this.model.jenis_kelamin  = response.data.siswa.jenis_kelamin;
          this.model.agama          = response.data.siswa.agama;
          this.model.nisn           = response.data.siswa.nisn;
          this.model.tahun_lulus    = response.data.siswa.tahun_lulus;
          this.model.sekolah        = response.data.siswa.sekolah;
          this.model.created_at     = response.data.siswa.created_at;
          this.model.updated_at     = response.data.siswa.updated_at;
        } else {
          alert('Failed');
        }
      })
      .catch(function(response) {
        alert('Break');
        window.location.href = '#/admin/siswa';
      })
  },
  data() {
    return {
      state: {},
      model: {
        user_id: "",
        nomor_un: "",
        nik: "",
        nama_siswa: "",
        alamat_kk: "",
        city_id: "",
        district_id: "",
        village_id: "",
        tempat_lahir: "",
        tgl_lahir: "",
        jenis_kelamin: "",
        agama: "",
        nisn: "",
        tahun_lulus: "",
        sekolah_id: "",
        created_at: "",
        updated_at: "",
        province_id: "",

      },
      user: [],
      sekolah: []
    }
  },
  methods: {
    reset() {
      axios.get('api/siswa/' + this.$route.params.id + '/edit')
        .then(response => {
          if (response.data.status == true) {
            this.model.label = response.data.siswa.label;
            this.model.description = response.data.siswa.description;
          } else {
            alert('Failed');
          }
        })
        .catch(function(response) {
          alert('Break ');
        });
    },
    back() {
      window.location = '#/admin/siswa';
    }
  }
}
</script>
