<script setup>
const model = defineModel({ type: [String, Number], default: '' })

defineProps({
  label: { type: String, default: '' },
  type: { type: String, default: 'text' },
  placeholder: { type: String, default: '' },
  error: { type: [String, Array], default: '' },
  hint: { type: String, default: '' },
  required: { type: Boolean, default: false },
})

const id = `input-${Math.random().toString(36).slice(2, 9)}`
</script>

<template>
  <div class="field">
    <label v-if="label" :for="id" class="field-label">
      {{ label }} <span v-if="required" class="wajib">*</span>
    </label>
    <textarea
      v-if="type === 'textarea'"
      :id="id"
      v-model="model"
      class="field-control"
      :class="{ invalid: error }"
      :placeholder="placeholder"
      rows="3"
    ></textarea>
    <input
      v-else
      :id="id"
      v-model="model"
      class="field-control"
      :class="{ invalid: error }"
      :type="type"
      :placeholder="placeholder"
      :required="required"
    />
    <small v-if="error" class="field-error">{{ Array.isArray(error) ? error[0] : error }}</small>
    <small v-else-if="hint" class="field-hint">{{ hint }}</small>
  </div>
</template>

<style scoped>
.field {
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.field-label {
  font-weight: 600;
  font-size: var(--font-size-sm);
}
.wajib {
  color: var(--color-danger);
}
.field-control {
  min-height: 40px;
  padding: var(--space-2) var(--space-3);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  background: var(--color-surface);
  color: var(--color-text);
  outline: none;
  transition:
    border-color 0.15s,
    box-shadow 0.15s;
}
.field-control:focus {
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px var(--color-primary-soft);
}
.field-control.invalid {
  border-color: var(--color-danger);
}
.field-error {
  color: var(--color-danger);
}
.field-hint {
  color: var(--color-text-muted);
}
</style>
