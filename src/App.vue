<template>
  <div id="app">
    <button @click="toggleData('todos')">Todos</button>
    <button @click="toggleData('posts')">Posts</button>
    <!-- Ganti konten yang ada dengan komponen Kegiatan -->
    <Kegiatan :data="currentData" />
  </div>
</template>

<script>
import Kegiatan from './components/Kegiatan.vue';

export default {
  name: 'App',
  components: {
    Kegiatan
  },
  data() {
    return {
      todos: [],
      posts: [],
      currentData: [] // Menyimpan data yang sedang ditampilkan
    };
  },
  created() {
    this.fetchData('todos'); // Mulai dengan menampilkan data todos saat aplikasi dimuat
  },
  methods: {
    fetchData(type) {
      fetch(`https://jsonplaceholder.typicode.com/${type}`)
        .then(response => response.json())
        .then(data => {
          this[type] = data;
          if (type === 'todos') {
            this.currentData = this.todos;
          } else {
            this.currentData = this.posts;
          }
        })
        .catch(error => {
          console.error(`Error fetching ${type}:`, error);
        });
    },
    toggleData(type) {
      this.currentData = []; // Kosongkan data yang ditampilkan
      this.fetchData(type); // Ambil data baru berdasarkan jenisnya
    }
  }
}
</script>
