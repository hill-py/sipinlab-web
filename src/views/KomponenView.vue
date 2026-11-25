<script setup>
import { ref } from 'vue'
import BaseButton from '@/components/base/BaseButton.vue'
import BaseInput from '@/components/base/BaseInput.vue'
import StatusBadge from '@/components/base/StatusBadge.vue'
import StatCard from '@/components/base/StatCard.vue'

const teksNormal = ref('')
const teksGalat = ref('OPT-001')
</script>

<template>
  <main class="wadah">
    <div class="page-header">
      <div>
        <h1>Design System & Komponen Dasar</h1>
        <p>Pameran varian tombol, isian, lencana status, dan kartu statistik SIPINLAB.</p>
      </div>
    </div>

    <section class="card bagian">
      <h2 class="card-title">BaseButton</h2>
      <div class="baris">
        <BaseButton variant="primary">Primary</BaseButton>
        <BaseButton variant="secondary">Secondary</BaseButton>
        <BaseButton variant="danger">Danger</BaseButton>
        <BaseButton variant="ghost">Ghost</BaseButton>
        <BaseButton size="sm">Kecil (sm)</BaseButton>
        <BaseButton :loading="true">Memuat</BaseButton>
        <BaseButton :disabled="true">Nonaktif</BaseButton>
      </div>
    </section>

    <section class="card bagian">
      <h2 class="card-title">BaseInput</h2>
      <div class="form-grid">
        <BaseInput
          v-model="teksNormal"
          label="Isian Normal"
          placeholder="Masukkan nama alat..."
          hint="Contoh teks petunjuk di bawah kolom."
        />
        <BaseInput
          v-model="teksGalat"
          label="Isian Galat (Validasi)"
          error="Kode sudah digunakan."
          required
        />
      </div>
    </section>

    <section class="card bagian">
      <h2 class="card-title">StatusBadge</h2>
      <div class="baris">
        <StatusBadge value="baik" />
        <StatusBadge value="rusak_ringan" />
        <StatusBadge value="rusak_berat" />
        <StatusBadge value="dipinjam" />
        <StatusBadge value="dikembalikan" />
        <StatusBadge value="terlambat" />
        <StatusBadge value="admin" />
        <StatusBadge value="petugas" />
      </div>
    </section>

    <section class="card bagian">
      <h2 class="card-title">StatCard</h2>
      <div class="grid-stat">
        <StatCard label="Jenis alat" :value="15" icon="box" tone="primary" />
        <StatCard
          label="Unit tersedia"
          :value="164"
          icon="check"
          tone="success"
          note="dari 169 unit"
        />
        <StatCard label="Sedang dipinjam" :value="2" icon="clipboard" tone="warning" />
        <StatCard label="Terlambat" :value="1" icon="alert" tone="danger" />
      </div>
    </section>
  </main>
</template>

<style scoped>
.wadah {
  max-width: 1040px;
  margin: 40px auto;
  padding: 0 16px;
}
.bagian {
  margin-bottom: var(--space-4);
}
.baris {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-3);
  align-items: center;
}
.grid-stat {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
  gap: var(--space-4);
}
</style>
