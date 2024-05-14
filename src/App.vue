<template>
  <div class="container">
    <h1 class="heading">What I Want to Do Today!!!</h1>

    <!-- Tombol Post -->
    <button @click="showPostSection" class="btn-post-section">Post</button>
    <!-- Tombol Todos -->
    <button @click="showTodosSection" class="btn-todos-section">Todos</button>

    <!-- Bagian Post -->
    <Post v-if="showPost" :users="users" @fetch-posts="fetchPosts" :posts="posts"/>

    <!-- Bagian Todos -->
    <Todos v-if="showTodos" :kegiatanList="kegiatanList" :filterAktif="filterAktif" @tambah-kegiatan="tambahKegiatan" @batalkan-kegiatan="batalkanKegiatan" @toggle-filter="toggleFilter"/>
  </div>
</template>

<script>
import Post from './components/Post.vue';
import Todos from './components/Todos.vue';

export default {
  components: {
    Post,
    Todos,
  },
  data() {
    return {
      kegiatanList: [],
      filterAktif: false,
      posts: [],
      users: [],
      showPost: false, // Menyimpan status tampilan bagian Post
      showTodos: true, // Menyimpan status tampilan bagian Todos (default ditampilkan saat halaman pertama dimuat)
    };
  },
  mounted() {
    // Load users from API
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(data => (this.users = data));
  },
  methods: {
    tambahKegiatan(namaKegiatan) {
      if (namaKegiatan.trim() !== '') {
        this.kegiatanList.push({ nama: namaKegiatan, selesai: false });
      }
    },
    batalkanKegiatan(index) {
      this.kegiatanList.splice(index, 1);
    },
    toggleFilter() {
      this.filterAktif = !this.filterAktif;
    },
    showPostSection() {
      this.showPost = true;
      this.showTodos = false;
    },
    showTodosSection() {
      this.showPost = false;
      this.showTodos = true;
    },
    fetchPosts(selectedUser) {
      if (selectedUser !== null) {
        fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser}`)
          .then(response => response.json())
          .then(data => (this.posts = data));
      }
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
