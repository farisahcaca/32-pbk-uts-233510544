<script setup>
import { ref } from 'vue'

const daftarKegiatan = ref([
  'Gym',
  'Traveling',
])
// Data untuk input kegiatan baru
const kegiatanBaru = ref('')

// Function untuk tambah kegiatan
function tambahKegiatan() {
  if (kegiatanBaru.value.trim() !== '') {
    daftarKegiatan.value.push(kegiatanBaru.value)
    kegiatanBaru.value = '' // Clear input setelah tambah
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
        {{ kegiatan }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
