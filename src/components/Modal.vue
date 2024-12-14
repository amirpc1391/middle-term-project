<script setup>
import Btn from "@/components/Btn.vue";
import formInput from "@/components/FormInput.vue";
import {computed, ref} from "vue";
const props=defineProps({
  isActiveModal: {
    type: Boolean,
    required: true,
  },
  modalStatusEdit: {
    type: Boolean,
    required: true,
  }
})
const modalStatusComputing =computed(()=>{
  if (props.modalStatusEdit){
    return "Edit"
  }else {
    return "Add"
  }
})
const priceModel=defineModel("price")
const descriptionModel=defineModel("description")
</script>

<template>
  <div :class="{'modal-section': true ,'modal-section--active':isActiveModal}">
    <div class="modal-section__content">
      <div class="modal-section__header">
        <h5 class="modal-section__title">{{modalStatusComputing}} transaction</h5>
        <Btn label="×" type="close" style="font-size: 1.5rem;" @click-btn="$emit('modal-close')"/>
      </div>
      <div class="modal-section__body">
        <form>
          <formInput input-id="price" label="price:" v-model="priceModel"/>
          <formInput input-id="description" label="description:" v-model="descriptionModel"/>
        </form>
      </div>
      <div class="modal-section__footer">
        <Btn :type="modalStatusComputing.toLocaleLowerCase()" :label="modalStatusComputing" @click-btn="$emit('modal-submit')"/>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-section {
  width: 100%;
  position: fixed;
  inset: 0;
  visibility: hidden;
  opacity: 0;
  transition: all .2s ease-in-out;
  background-color: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(10px);
  padding: 3rem;
}

.modal-section--active {
  visibility: visible;
  opacity: 1;
  padding: 5rem;
}

.modal-section__content {
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

.modal-section__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid var(--color_dee2e6);
  border-bottom-color: var(--color_495057);
  padding: 1.5rem;
  color: var(--color_adb5bd);
}

.modal-section__body {
  padding: 1.5rem;
}

.modal-section__footer {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  border-top: 1px solid var(--color_495057);
  padding: 1rem 1.5rem;
}
</style>