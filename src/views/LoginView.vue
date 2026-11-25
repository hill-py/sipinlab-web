<script setup>
import { reactive } from 'vue'
import BaseInput from '@/components/base/BaseInput.vue'
import BaseButton from '@/components/base/BaseButton.vue'
import logo from '@/assets/logo.svg'

const form = reactive({ email: '', password: '' })

function masuk() {
  alert(`Surel: ${form.email}\nProses masuk ke API dibuat di Modul 6.`)
}
</script>

<template>
  <div class="login-page">
    <section class="brand-panel">
      <img :src="logo" alt="" width="64" height="64" />
      <h1>SIPINLAB</h1>
      <p>Sistem Informasi Peminjaman Alat Laboratorium</p>
      <ul>
        <li>Pantau stok alat secara langsung</li>
        <li>Catat peminjaman dan pengembalian</li>
        <li>Ketahui peminjaman yang terlambat</li>
      </ul>
    </section>
    <section class="form-panel">
      <form class="login-card" @submit.prevent="masuk">
        <h2>Masuk</h2>
        <p class="text-muted">Gunakan akun petugas laboratorium Anda.</p>
        <BaseInput
          v-model="form.email"
          label="Surel"
          type="email"
          placeholder="nama@sipinlab.test"
          required
        />
        <BaseInput
          v-model="form.password"
          label="Kata sandi"
          type="password"
          placeholder="••••••••"
          required
        />
        <BaseButton type="submit" block>Masuk</BaseButton>
        <p class="demo">Akun latihan: <code>admin@sipinlab.test</code> / <code>password</code></p>
      </form>
    </section>
  </div>
</template>

<style scoped>
.login-page {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.brand-panel {
  background: linear-gradient(160deg, var(--color-primary) 0%, var(--color-sidebar) 100%);
  color: #fff;
  padding: 64px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: var(--space-3);
}
.brand-panel h1 {
  font-size: 40px;
  letter-spacing: 0.06em;
}
.brand-panel p {
  margin: 0;
  font-size: var(--font-size-md);
  opacity: 0.9;
}
.brand-panel ul {
  margin: var(--space-5) 0 0;
  padding-left: 20px;
  line-height: 2;
  opacity: 0.9;
}
.form-panel {
  display: grid;
  place-items: center;
  padding: var(--space-5);
}
.login-card {
  width: 100%;
  max-width: 400px;
  display: flex;
  flex-direction: column;
  gap: var(--space-4);
}
.login-card h2 {
  font-size: var(--font-size-xl);
}
.login-card > p {
  margin: -8px 0 0;
}
.demo {
  font-size: var(--font-size-xs);
  color: var(--color-text-muted);
  text-align: center;
}
@media (max-width: 860px) {
  .login-page {
    grid-template-columns: 1fr;
  }
  .brand-panel {
    padding: var(--space-6) var(--space-5);
  }
  .brand-panel ul {
    display: none;
  }
}
</style>
