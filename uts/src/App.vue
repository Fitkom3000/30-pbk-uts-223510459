<template>
  <div class="container">
    <h1 class="heading">Aplikasi Pengingat Kegiatan</h1>

    <div class="input-section">
      <h2 class="section-title">Tambah Kegiatan Baru</h2>
      <input type="text" v-model="namaKegiatan" placeholder="Nama Kegiatan" class="input-kegiatan">
      <button @click="tambahKegiatan" class="btn-tambah">Tambah</button>
    </div>

    <div class="list-section">
      <h2 class="section-title">Daftar Kegiatan</h2>
      <ul>
        <li v-for="(kegiatan, index) in filteredKegiatanList" :key="index" class="daftar-kegiatan">
          <span :style="{ textDecoration: kegiatan.selesai ? 'line-through' : 'none' }">{{ kegiatan.nama }}</span>
          <button @click="batalkanKegiatan(index)" class="btn-batalkan">Batalkan</button>
          <input type="checkbox" v-model="kegiatan.selesai" class="checkbox-selesai">
        </li>
      </ul>
      <button @click="toggleFilter" class="btn-filter" :class="{ active: filterAktif }">Filter Belum Selesai</button>
    </div>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 20px;
  gap: 20px;
}

.heading {
  font-size: 32px;
  font-weight: bold;
}

.input-section {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.section-title {
  font-size: 24px;
}

.input-kegiatan {
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ced4da;
  width: 300px;
  box-sizing: border-box;
}

.btn-tambah {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
}

.list-section {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.daftar-kegiatan {
  display: top;
  justify-content: space-between;
  align-items: left;
  padding: 8px;
  background-color: #000000;
  border-radius: 4px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.btn-batalkan, .btn-filter {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 4px 8px;
  border-radius: 4px;
  cursor: pointer;
}

.checkbox-selesai {
  margin-left: 8px;
}

.btn-filter.active {
  background-color: #28a745;
}
</style>

<script>
export default {
  data() {
    return {
      namaKegiatan: '',
      kegiatanList: [],
      filterAktif: false,
    };
  },
  computed: {
    filteredKegiatanList() {
      if (this.filterAktif) {
        return this.kegiatanList.filter(kegiatan => !kegiatan.selesai);
      } else {
        return this.kegiatanList;
      }
    }
  },
  methods: {
    tambahKegiatan() {
      if (this.namaKegiatan.trim() !== '') {
        this.kegiatanList.push({ nama: this.namaKegiatan, selesai: false });
        this.namaKegiatan = '';
      }
    },
    batalkanKegiatan(index) {
      this.kegiatanList.splice(index, 1);
    },
    toggleFilter() {
      this.filterAktif = !this.filterAktif;
    },
  },
};
</script>
