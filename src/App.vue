<template>
  <div class="container">
    <h1 class="heading">To Do List!!!</h1>

    <div class="input-section">
      <h2 class="section-title">Add List</h2>
      <div class="input-container">
        <input type="text" v-model="namaKegiatan" placeholder="Apa Kegiatanmu hari ini!" class="input-kegiatan">
        <button @click="tambahKegiatan" class="btn-tambah">Tambahkan</button>
      </div>
    </div>

    <div class="list-section">
      <h2 class="section-title">Daftar Kegiatan</h2>
      <ul>
        <li v-for="(kegiatan, index) in filteredKegiatanList" :key="index" class="daftar-kegiatan">
          <div class="kegiatan-info">
            <span class="span" :style="{ textDecoration: kegiatan.selesai ? 'line-through' : 'none' }">{{ kegiatan.nama }}</span>
            <button @click="batalkanKegiatan(index)" class="btn-batalkan">Batalkan</button>
          </div>
          <input type="checkbox" v-model="kegiatan.selesai" class="checkbox-selesai">
        </li>
      </ul>
      <button @click="toggleFilter" class="btn-filter" :class="{ active: filterAktif }">Check List !!</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 20px;
  background-image: url('foto1.JPEG');
  background-size: cover;
  background-position: center;
  background-repeat: fixed;
}


.heading {
  font-size: 32px;
  font-weight: bold;
  margin-bottom: 20px;
  color: #333333;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}

.section-title {
  font-size: 24px;
  margin-bottom: 10px;
}

.input-container {
  display: flex;
  gap: 10px;
  align-items: center;
}

.input-kegiatan {
  flex: 1;
  padding: 10px;
  border-radius: 100px; /* Agar input lebih bulat */
  border: 1px solid #ced4da;
}

.btn-tambah {
  background-color: #00ff00;
  color: white;
  border: none;
  padding: 5px 16px;
  border-radius: 10px;
  cursor: pointer;
}

.list-section {
  margin-top: 20px;
  width: 100%; /* Agar lebar list-section mengisi penuh container */
}

.daftar-kegiatan {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #ffffff;
  border-radius: 4px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  margin-bottom: 10px;
}

.kegiatan-info {
  display: flex;
  align-items: center;
}

.span {
  color: #000000;
  margin-right: 10px;
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
  margin-left: 10px;
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
