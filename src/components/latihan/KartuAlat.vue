<script setup>
defineProps({
  kode: { type: String, required: true },
  nama: { type: String, required: true },
  tersedia: { type: Number, default: 0 },
  total: { type: Number, default: 0 },
})

const emit = defineEmits(['pinjam'])
</script>

<template>
  <article class="kartu" :class="{ habis: tersedia === 0 }">
    <span class="kode">{{ kode }}</span>
    <h3>{{ nama }}</h3>
    <p>
      Tersedia <strong>{{ tersedia }}</strong> dari {{ total }} unit
    </p>
    <p v-if="tersedia === 0" class="label-habis">Stok habis</p>
    <button :disabled="tersedia === 0" @click="emit('pinjam', kode)">Pinjam 1 unit</button>
  </article>
</template>

<style scoped>
.kartu {
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 16px;
  background: #fff;
}
.kartu.habis {
  opacity: 0.6;
}
.kode {
  font-size: 12px;
  color: #64748b;
}
h3 {
  margin: 4px 0 8px;
}
.label-habis {
  color: #b91c1c;
  font-weight: 600;
}
button {
  margin-top: 8px;
  padding: 8px 12px;
  border: 0;
  border-radius: 8px;
  background: #0e7c66;
  color: #fff;
  cursor: pointer;
}
button:disabled {
  background: #94a3b8;
  cursor: not-allowed;
}
</style>
