<template>
  <div class="input-section">
    <h2 class="section-title">Post</h2>
    <select v-model="selectedUser" class="select-user">
      <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
    </select>
    <button @click="post" class="btn-post">Post</button>
    <div class="list-section">
      <h2 class="section-title">Daftar Postingan</h2>
      <ul>
        <li v-for="(post, index) in posts" :key="index" class="daftar-post">
          <span>{{ post.title }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['users', 'posts'],
  data() {
    return {
      selectedUser: null,
    };
  },
  methods: {
    post() {
      this.$emit('fetch-posts', this.selectedUser);
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
