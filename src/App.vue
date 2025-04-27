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
.selesai {
  text-decoration: line-through;
  color: #999;
  transition: all 0.3s ease;
}
li:hover {
  background-color: #eef6f6;
}

</style>
