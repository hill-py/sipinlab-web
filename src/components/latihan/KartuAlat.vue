<script setup>
import { computed } from 'vue'

const props = defineProps({
  kode: { type: String, required: true },
  nama: { type: String, required: true },
  tersedia: { type: Number, default: 0 },
  total: { type: Number, default: 0 },
  kondisi: {
    type: String,
    default: 'baik',
    validator: (v) => ['baik', 'rusak_ringan', 'rusak_berat'].includes(v),
  },
})

const emit = defineEmits(['pinjam', 'kembali'])

const labelKondisi = computed(() => {
  const daftar = {
    baik: 'Baik',
    rusak_ringan: 'Rusak Ringan',
    rusak_berat: 'Rusak Berat',
  }
  return daftar[props.kondisi] || props.kondisi
})
</script>

<template>
  <article class="kartu" :class="{ habis: tersedia === 0 }">
    <div class="header-kartu">
      <span class="kode">{{ kode }}</span>
      <span class="badge-kondisi" :class="kondisi">{{ labelKondisi }}</span>
    </div>
    <h3>{{ nama }}</h3>
    <p>
      Tersedia <strong>{{ tersedia }}</strong> dari {{ total }} unit
    </p>
    <p v-if="tersedia === 0" class="label-habis">Stok habis</p>
    <div class="aksi">
      <button class="btn-pinjam" :disabled="tersedia === 0" @click="emit('pinjam', kode)">
        Pinjam 1 unit
      </button>
      <button class="btn-kembali" :disabled="tersedia >= total" @click="emit('kembali', kode)">
        Kembalikan 1 unit
      </button>
    </div>
  </article>
</template>

<style scoped>
.kartu {
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 16px;
  background: #fff;
  display: flex;
  flex-direction: column;
}
.kartu.habis {
  opacity: 0.75;
}
.header-kartu {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 8px;
}
.kode {
  font-size: 12px;
  color: #64748b;
}
.badge-kondisi {
  font-size: 11px;
  font-weight: 600;
  padding: 2px 8px;
  border-radius: 999px;
}
.badge-kondisi.baik {
  background: #dcfce7;
  color: #166534;
}
.badge-kondisi.rusak_ringan {
  background: #fef3c7;
  color: #92400e;
}
.badge-kondisi.rusak_berat {
  background: #fee2e2;
  color: #991b1b;
}
h3 {
  margin: 8px 0;
}
.label-habis {
  color: #b91c1c;
  font-weight: 600;
  margin: 0 0 8px;
}
.aksi {
  margin-top: auto;
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding-top: 8px;
}
button {
  padding: 8px 12px;
  border: 0;
  border-radius: 8px;
  color: #fff;
  cursor: pointer;
  font-weight: 500;
}
.btn-pinjam {
  background: #0e7c66;
}
.btn-kembali {
  background: #2563eb;
}
button:disabled {
  background: #94a3b8;
  cursor: not-allowed;
}
</style>
