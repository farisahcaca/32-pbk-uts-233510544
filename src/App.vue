<script setup>
import { ref } from 'vue'

const daftarKegiatan = ref([
  'Gym',
  'Traveling',
])
</script>

<template>
 <div class="app">
    <h1>Daftar Kegiatan</h1>
    <ul>
      <li v-for="(kegiatan, index) in daftarKegiatan" :key="index">
        {{ kegiatan }}
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
