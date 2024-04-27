<template>
  <div id="app">
    <!-- Ganti konten yang ada dengan komponen Kegiatan -->
    <Kegiatan />
  </div>
</template>

<script>
// Impor komponen Kegiatan.vue
import Kegiatan from './components/Kegiatan.vue'

export default {
  name: 'App',
  components: {
    // Tambahkan komponen Kegiatan ke dalam daftar komponen
    Kegiatan
  }
}
</script>

<style>
/* Gaya untuk aplikasi Vue Anda */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
