<script setup>
import { ref } from 'vue'

const daftarKegiatan = ref([
{ nama: 'Traveling', selesai: false },
{ nama: 'Gym', selesai: true }
])
// Data untuk input kegiatan baru
const kegiatanBaru = ref('')

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
    <ul>
      <li v-for="(kegiatan, index) in daftarKegiatan" :key="index">
        <input type="checkbox" v-model="kegiatan.selesai" />
        <span :class="{ selesai: kegiatan.selesai }">{{ kegiatan.nama }}</span>
        <button @click="hapusKegiatan(index)">🗑️</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
