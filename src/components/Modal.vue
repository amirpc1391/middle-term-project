<script setup>
import Btn from "@/components/Btn.vue";
import formInput from "@/components/FormInput.vue";
</script>

<template>
  <div class="modal">
    <div class="modal__header">
      <h5 class="modal__title">Add transaction</h5>
      <Btn label="×" type="close" style="font-size: 1.5rem;"/>
    </div>
    <div class="modal__body">
      <form>
        <formInput input-id="price" label="price:"/>
        <formInput input-id="description" label="description:"/>
      </form>
    </div>
    <div class="modal__footer">
      <Btn type="edit" label="Add"/>
    </div>
  </div>
</template>

<style scoped>
.modal {
  max-width: 30rem;
  display: flex;
  flex-direction: column;
  width: 100%;
  pointer-events: auto;
  background-color: var(--color_343a40);
  background-clip: padding-box;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 0.5rem;
  outline: 0;
  margin: 1.75rem auto;
}

.modal__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid var(--color_dee2e6);
  border-bottom-color: var(--color_495057);
  padding: 1.5rem;
  color: var(--color_adb5bd);
}
.modal__body {
  padding: 1.5rem;
}

.modal__footer {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  border-top: 1px solid var(--color_495057);
  padding: 1rem 1.5rem;
}
</style>