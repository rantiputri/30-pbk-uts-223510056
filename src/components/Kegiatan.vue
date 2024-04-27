<template>
  <div class="container">
    <h2 class="judul">Daftar Kegiatan</h2>
    <ul class="kegiatan-list">
      <li v-for="kegiatan in kegiatan" :key="kegiatan.id" class="kegiatan-item">
        <div class="kegiatan-info">
          <div class="kegiatan-column nama">
            <div class="column-title">Nama Kegiatan</div>
            <div class="kegiatan-nama">{{ kegiatan.nama }}</div>
          </div>
          <div class="kegiatan-column tanggal">
            <div class="column-title">Tanggal</div>
            <div class="kegiatan-tanggal">{{ kegiatan.tanggal }}</div>
          </div>
          <div class="kegiatan-column actions">
            <div class="column-title">Aksi</div>
            <div class="kegiatan-actions">
              <button @click="hapusKegiatan(kegiatan.id)" class="btn btn-danger">Batal</button>
            </div>
          </div>
          <div class="kegiatan-column done">
            <div class="column-title">Done</div>
            <div class="kegiatan-done">
              <label class="switch">
                <input type="checkbox" v-model="kegiatan.selesai">
                <span class="slider round"></span>
              </label>
            </div>
          </div>
        </div>
      </li>
    </ul>

    <h3>Tambah Kegiatan Baru</h3>
    <form @submit.prevent="tambahKegiatan" class="form-tambah">
      <div class="form-group">
        <label for="namaKegiatan">Nama Kegiatan:</label>
        <input type="text" id="namaKegiatan" v-model="newKegiatan.nama" required class="form-control">
      </div>
      <div class="form-group">
        <label for="tanggalKegiatan">Tanggal:</label>
        <input type="date" id="tanggalKegiatan" v-model="newKegiatan.tanggal" required class="form-control">
      </div>
      <div class="form-group">
        <label for="deskripsiKegiatan">Deskripsi:</label>
        <textarea id="deskripsiKegiatan" v-model="newKegiatan.deskripsi" rows="4" class="form-control"></textarea>
      </div>
      <button type="submit" class="btn btn-primary">Tambah</button>
    </form>

    <h3>Filter Kegiatan</h3>
    <div class="filter-buttons">
      <button @click="filterSelesai = 'belum-selesai'" class="btn btn-secondary">Belum Selesai</button>
      <button @click="filterSelesai = 'selesai'" class="btn btn-secondary">Selesai</button>
      <button @click="filterSelesai = 'semua'" class="btn btn-secondary">Semua</button>
    </div>
    <ul class="kegiatan-list">
      <li v-for="kegiatan in kegiatanDifilter" :key="kegiatan.id" class="kegiatan-item">
        <div class="kegiatan-info">
          <div class="kegiatan-nama">{{ kegiatan.nama }}</div>
          <div class="kegiatan-tanggal">{{ kegiatan.tanggal }}</div>
          <div class="kegiatan-actions">
            <span class="kegiatan-status">{{ kegiatan.selesai ? 'Selesai' : 'Belum Selesai' }}</span>
          </div>
        </div>
      </li>
    </ul>
  </div>


  <div class="container">
    <!-- Konten sebelumnya -->

    <!-- Footer -->
    <footer class="footer">
      <p>&copy; 2024 Ranti Putri Nian</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'DaftarKegiatan',
  data() {
    return {
      kegiatan: [
        { id: 1, nama: "Belajar Vue.js", tanggal: "2024-04-12", selesai: false, deskripsi: " " },
        { id: 2, nama: "Membeli bahan makanan", tanggal: "2024-04-13", selesai: true, deskripsi: " " },
        { id: 2, nama: "Membeli bahan radikal", tanggal: "2024-04-14", selesai: true, deskripsi: " " },
      ],
      newKegiatan: {
        nama: "",
        tanggal: "",
        selesai: false,
        deskripsi: "",
      },
      filterSelesai: "semua",
    };
  },
  methods: {
    tambahKegiatan() {
      if (this.newKegiatan.nama === "" || this.newKegiatan.tanggal === "") {
        alert("Nama dan tanggal kegiatan wajib diisi!");
        return;
      }
      
      this.kegiatan.push({
        id: Date.now(),
        ...this.newKegiatan,
      });

      this.newKegiatan = {
        nama: "",
        tanggal: "",
        selesai: false,
        deskripsi: "",
      };
    },
    hapusKegiatan(id) {
      const index = this.kegiatan.findIndex(kegiatan => kegiatan.id === id);
      if (index > -1) {
        this.kegiatan.splice(index, 1);
      }
    },
    toggleSelesai(kegiatan) {
      kegiatan.selesai = !kegiatan.selesai;
    }
  },
  computed: {
    kegiatanDifilter() {
      switch (this.filterSelesai) {
        case "belum-selesai":
          return this.kegiatan.filter(kegiatan => !kegiatan.selesai);
        case "selesai":
          return this.kegiatan.filter(kegiatan => kegiatan.selesai);
        default:
          return this.kegiatan;
      }
    }
  }
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  color: #fff;
  background-color: #222;
}

.container {
  background: linear-gradient(45deg, #222 0%, #000 100%);

  border: 1px solid #333;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(211, 35, 234, 0.2);
  padding: 30px;
  margin: 20px auto;
  max-width: 800px; 
  color: white;
}

.name-app {
  color: #f0f0f0;
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 20px;
}

.judul {
  color: #fff;
  text-align: center;
  font-size: 20px;
  margin-bottom: 20px;
}

/* Judul */
h3 {
  color: #fff;
  text-align: center;
  margin-bottom: 20px;
}

/* Formulir */
.form-group {
  color: #fff;
  margin-bottom: 15px;
}

.form-control {
  width: 100%;
  padding: 10px;
  border: 1px solid #666;
  border-radius: 5px;
  background-color: #333;
  color: #fff;
  outline: none;
}

.btn {
  cursor: pointer;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  font-weight: bold;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: #444;
}

.btn-primary {
  background-color: #4CAF50; /* Hijau */
  color: white;
}

.btn-secondary {
  background-color: #007bff; /* Biru */
  color: white;
}

.btn-danger {
  background-color: #dc3545; /* Merah */
  color: white;
}

/* Filter */
.filter-buttons button {
  margin-right: 10px;
  background-color: #333;
  color: #fff;
  padding: 10px 15px;
  border: 1px solid #666;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

.filter-buttons button:hover {
  background-color: #444;
}

.kegiatan-list {
  list-style-type: none;
  padding: 0;
  text-align: center; /* Rata tengah isi daftar kegiatan */
}

.kegiatan-item {
  margin-bottom: 20px;
  padding: 20px;
  background-color: #444;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
 border: 1px solid #ffffff;
}

.kegiatan-info {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
  align-items: center;
  justify-items: center; 
}

.kegiatan-detail {
  display: flex;
  flex-direction: column;
}

.kegiatan-nama {
  font-weight: bold;
  margin-bottom: 5px;
  color: #fff;
}

.kegiatan-tanggal {
  color: #fff;
  margin-bottom: 5px;
}

.kegiatan-actions {
  display: flex;
  align-items: center;
  justify-content: center; 
}

.toggle-checkbox {
  display: none;
}

.toggle-checked .slider {
  background-color: #2196F3;
}

.toggle-checked input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Footer */
.footer {
  background-color: #333333;
  color: white;
  padding: 20px;
  text-align: center;
  /* Menambahkan border untuk footer */
  border: 1px solid #ccc;
  border-radius: 10px;
}

.kegiatan-column {
  padding: 10px;
  justify-self: center; /* Rata tengah konten dalam setiap kolom */
}

.column-title {
  font-weight: bold;
  margin-bottom: 5px;
  text-align: center; /* Menengahkan judul */
}

.nama {
  grid-column: 1;
}

.tanggal {
  grid-column: 2;
}

.actions {
  grid-column: 3;
}

.done {
  grid-column: 4;
  text-align: center;
}
</style>
