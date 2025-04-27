<script setup>
import { ref,computed } from 'vue'

const daftarKegiatan = ref([
{ nama: 'Traveling', selesai: false },
{ nama: 'Gym', selesai: true }
])
// Data untuk input kegiatan baru
const kegiatanBaru = ref('')

// Filter untuk hanya tampilkan yang belum selesai
const tampilkanBelumSelesai = ref(false)
// Computed untuk filter data
const kegiatanTampil = computed(() => {
  if (tampilkanBelumSelesai.value) {
    return daftarKegiatan.value.filter(kegiatan => !kegiatan.selesai)
  }
  return daftarKegiatan.value
})

// Function untuk tambah kegiatan
function tambahKegiatan() {
  if (kegiatanBaru.value.trim() !== '') {
    daftarKegiatan.value.push({
      nama: kegiatanBaru.value,
      selesai: false
    })
    kegiatanBaru.value = ''
  }
}
//Function untuk hapus kegiatan
function hapusKegiatan(index) {
  if (confirm('Yakin ingin menghapus kegiatan ini?')) {
    daftarKegiatan.value.splice(index, 1)
  }
}

</script>

<template>
 <div class="app">
  <h1>📋MyActivity📌</h1>
  <form @submit.prevent="tambahKegiatan">
      <input
        type="text"
        v-model="kegiatanBaru"
        placeholder="Tambah kegiatan..."
      />
      <button type="submit">Tambah</button>
    </form>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="tampilkanBelumSelesai" />
        Tampilkan kegiatan yang belum selesai
      </label>
    </div>

    <ul>
      <li v-for="(kegiatan, index) in kegiatanTampil" :key="index">
        <input type="checkbox" v-model="kegiatan.selesai" />
        <span :class="{ selesai: kegiatan.selesai }">{{ kegiatan.nama }}</span>
        <button @click="hapusKegiatan(index)">🗑️</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.app {
  max-width: 400px;
  margin: 50px auto;
  padding: 30px;
  background: #f4f1eb;
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

h1 {
  text-align: center;
  font-size: 2.0rem;
  margin-bottom: 50px;
  color: #6f4f37;
  font-weight: bold;
}

form {
  display: flex;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 2px solid #d2b48c;
  border-radius: 8px 0 0 8px;
  font-size: 16px;
  outline: none;
}

button[type="submit"] {
  background-color: #8b5e3c;
  border: none;
  color: white;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 0 8px 8px 0;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s;
}

button[type="submit"]:hover {
  background-color: #6a4e2f;
  transform: scale(1.05);
}

.filter {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  gap: 10px;
  font-size: 14px;
  color: #6f4f37;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background: #fff5e1;
  margin-bottom: 10px;
  padding: 12px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

li:hover {
  transform: translateY(-2px);
}

li input[type="checkbox"] {
  margin-right: 10px;
}

li span {
  flex: 1;
  text-align: left;
  font-size: 16px;
  color: #6f4f37;
}

li button {
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
  color: #8b5e3c;
  transition: color 0.3s, transform 0.2s;
}

li button:hover {
  color: #6a4e2f;
  transform: scale(1.2);
}
.selesai {
  text-decoration: line-through;
  color: #999;
  transition: all 0.3s ease;
}
</style>
