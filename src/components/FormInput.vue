<script setup>
defineProps({
  label: {
    type: String,
    required: true,
  },
  inputId: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <div class="form-input">
    <label :for="inputId" class="form-input__label">{{ label }}</label>
    <input
        type="text"
        :id="inputId"
        class="form-input__input"
    />
  </div>
</template>

<style scoped>

.form-input {
  margin-bottom: 1rem;
  color: var(--color_adb5bd);
}
.form-input__label {
  display: inline-block;
  padding: 0.4rem 0;
  line-height: 1.5;
}
.form-input__input {
  display: block;
  width: 100%;
  font-size: 0.9rem;
  height: 2.5rem;
  padding: 0.4rem 0.8rem;
  background-color: transparent;
  border: 1px solid var(--color_495057);
  border-radius: 0.25rem;
  transition: all 0.15s ease-in-out;
  color: var(--color_ced4da);
  outline: none;
}
.form-input__input:focus {
  border-color: var(--color_65caec);
  color: var(--color_ced4da);
  background: var(--color_42484f);
}
</style>