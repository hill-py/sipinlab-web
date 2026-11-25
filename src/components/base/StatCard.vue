<script setup>
import AppIcon from './AppIcon.vue'

defineProps({
  label: { type: String, required: true },
  value: { type: [Number, String], default: 0 },
  icon: { type: String, default: 'box' },
  tone: { type: String, default: 'primary' },
  note: { type: String, default: '' },
})
</script>

<template>
  <div class="stat card">
    <div class="stat-icon" :class="`tone-${tone}`">
      <AppIcon :name="icon" :size="22" />
    </div>
    <div>
      <p class="stat-label">{{ label }}</p>
      <p class="stat-value">{{ value }}</p>
      <p v-if="note" class="stat-note">{{ note }}</p>
    </div>
  </div>
</template>

<style scoped>
.stat {
  display: flex;
  gap: var(--space-4);
  align-items: flex-start;
}
.stat-icon {
  width: 44px;
  height: 44px;
  border-radius: var(--radius-md);
  display: grid;
  place-items: center;
  flex-shrink: 0;
}
.tone-primary {
  background: var(--color-primary-soft);
  color: var(--color-primary);
}
.tone-success {
  background: var(--color-success-soft);
  color: var(--color-success);
}
.tone-warning {
  background: var(--color-warning-soft);
  color: var(--color-warning);
}
.tone-danger {
  background: var(--color-danger-soft);
  color: var(--color-danger);
}
.stat-label {
  margin: 0;
  color: var(--color-text-muted);
  font-weight: 500;
}
.stat-value {
  margin: 2px 0 0;
  font-size: var(--font-size-xl);
  font-weight: 700;
}
.stat-note {
  margin: 0;
  font-size: var(--font-size-xs);
  color: var(--color-text-muted);
}
</style>
