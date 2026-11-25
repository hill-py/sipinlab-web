<script setup>
defineProps({
  variant: { type: String, default: 'primary' },
  size: { type: String, default: 'md' },
  type: { type: String, default: 'button' },
  loading: { type: Boolean, default: false },
  disabled: { type: Boolean, default: false },
  block: { type: Boolean, default: false },
})
</script>

<template>
  <button
    :type="type"
    class="btn"
    :class="[`btn-${variant}`, `btn-${size}`, { 'btn-block': block }]"
    :disabled="disabled || loading"
  >
    <span v-if="loading" class="spinner" aria-hidden="true"></span>
    <slot />
  </button>
</template>

<style scoped>
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  border: 1px solid transparent;
  border-radius: var(--radius-md);
  font-weight: 600;
  cursor: pointer;
  white-space: nowrap;
  transition:
    background-color 0.15s,
    border-color 0.15s;
}
.btn-md {
  height: 40px;
  padding: 0 var(--space-4);
}
.btn-sm {
  height: 32px;
  padding: 0 var(--space-3);
  font-size: var(--font-size-xs);
}
.btn-block {
  width: 100%;
}
.btn-primary {
  background: var(--color-primary);
  color: #fff;
}
.btn-primary:hover:not(:disabled) {
  background: var(--color-primary-hover);
}
.btn-secondary {
  background: var(--color-surface);
  border-color: var(--color-border);
  color: var(--color-text);
}
.btn-secondary:hover:not(:disabled) {
  border-color: var(--color-primary);
  color: var(--color-primary);
}
.btn-danger {
  background: var(--color-danger-soft);
  color: var(--color-danger);
}
.btn-danger:hover:not(:disabled) {
  background: #fecaca;
}
.btn-ghost {
  background: transparent;
  color: var(--color-text-muted);
}
.btn-ghost:hover:not(:disabled) {
  background: var(--color-bg);
  color: var(--color-text);
}
.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
.spinner {
  width: 14px;
  height: 14px;
  border: 2px solid currentColor;
  border-right-color: transparent;
  border-radius: 50%;
  animation: putar 0.7s linear infinite;
}
@keyframes putar {
  to {
    transform: rotate(360deg);
  }
}
</style>
