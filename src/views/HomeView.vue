<script setup>
import { computed, ref } from 'vue'
import KartuAlat from '@/components/latihan/KartuAlat.vue'

const judul = 'Latihan Vue: Daftar Alat Laboratorium'
const kataKunci = ref('')
const daftarAlat = ref([
  { kode: 'OPT-001', nama: 'Mikroskop Binokuler', tersedia: 8, total: 10 },
  { kode: 'UKR-001', nama: 'Timbangan Analitik', tersedia: 1, total: 3 },
  { kode: 'ELK-001', nama: 'Multimeter Digital', tersedia: 17, total: 20 },
  { kode: 'PMN-002', nama: 'Oven Laboratorium', tersedia: 0, total: 2 },
])

const alatTampil = computed(() =>
  daftarAlat.value.filter((alat) =>
    alat.nama.toLowerCase().includes(kataKunci.value.toLowerCase()),
  ),
)

const totalTersedia = computed(() => daftarAlat.value.reduce((jumlah, a) => jumlah + a.tersedia, 0))

function pinjam(kode) {
  const alat = daftarAlat.value.find((a) => a.kode === kode)
  if (alat && alat.tersedia > 0) alat.tersedia--
}
</script>

<template>
  <main class="wadah">
    <h1>{{ judul }}</h1>
    <p>
      Total unit tersedia: <strong>{{ totalTersedia }}</strong>
    </p>
    <input v-model="kataKunci" class="cari" placeholder="Cari alat..." />
    <p class="ketikan">Anda mengetik: "{{ kataKunci }}"</p>

    <div class="grid">
      <KartuAlat v-for="alat in alatTampil" :key="alat.kode" v-bind="alat" @pinjam="pinjam" />
    </div>
    <p v-if="alatTampil.length === 0">Alat tidak ditemukan.</p>
  </main>
</template>

<style scoped>
.wadah {
  max-width: 960px;
  margin: 40px auto;
  padding: 0 16px;
  font-family: system-ui, sans-serif;
}
.cari {
  width: 100%;
  padding: 10px 12px;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-size: 16px;
}
.ketikan {
  color: #64748b;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 16px;
}
</style>
