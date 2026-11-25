<script setup>
import { computed } from 'vue'

const props = defineProps({ value: { type: String, required: true } })

const peta = {
  baik: { teks: 'Baik', tone: 'success' },
  rusak_ringan: { teks: 'Rusak ringan', tone: 'warning' },
  rusak_berat: { teks: 'Rusak berat', tone: 'danger' },
  dipinjam: { teks: 'Dipinjam', tone: 'info' },
  dikembalikan: { teks: 'Dikembalikan', tone: 'success' },
  terlambat: { teks: 'Terlambat', tone: 'danger' },
  admin: { teks: 'Admin', tone: 'info' },
  petugas: { teks: 'Petugas', tone: 'success' },
}

const badge = computed(() => peta[props.value] ?? { teks: props.value, tone: 'info' })
</script>

<template>
  <span class="badge" :class="`badge-${badge.tone}`">{{ badge.teks }}</span>
</template>

<style scoped>
.badge {
  display: inline-block;
  padding: 2px 10px;
  border-radius: 999px;
  font-size: var(--font-size-xs);
  font-weight: 600;
  white-space: nowrap;
}
.badge-success {
  background: var(--color-success-soft);
  color: var(--color-success);
}
.badge-warning {
  background: var(--color-warning-soft);
  color: var(--color-warning);
}
.badge-danger {
  background: var(--color-danger-soft);
  color: var(--color-danger);
}
.badge-info {
  background: var(--color-info-soft);
  color: var(--color-info);
}
</style>
