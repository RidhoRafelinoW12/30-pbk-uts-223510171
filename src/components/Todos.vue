<template>
  <div>
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

<script>
export default {
  props: ['kegiatanList', 'filterAktif'],
  data() {
    return {
      namaKegiatan: '',
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
      this.$emit('tambah-kegiatan', this.namaKegiatan);
      this.namaKegiatan = '';
    },
    batalkanKegiatan(index) {
      this.$emit('batalkan-kegiatan', index);
    },
    toggleFilter() {
      this.$emit('toggle-filter');
    },
  },
};
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.heading {
  text-align: center;
  margin-bottom: 20px;
}

.btn-post-section,
.btn-todos-section {
  display: inline-block;
  margin-right: 10px;
  padding: 8px 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.input-section {
  margin-bottom: 20px;
}

.section-title {
  margin-bottom: 10px;
}

.input-container {
  display: flex;
  margin-bottom: 10px;
}

.input-kegiatan {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 10px;
}

.btn-tambah,
.btn-post,
.btn-batalkan,
.btn-filter {
  padding: 8px 16px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-right: 10px;
}

.list-section {
  margin-bottom: 20px;
}

.daftar-kegiatan {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.kegiatan-info {
  flex: 1;
}

.checkbox-selesai {
  margin-right: 10px;
}

.daftar-post {
  margin-bottom: 5px;
}

.active {
  background-color: #0056b3;
}
</style>
