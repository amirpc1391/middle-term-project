<script setup>

import Btn from "@/components/Btn.vue";

const props = defineProps( {

  title : {
    type : String ,
    default : "Modal Name"
  } ,
  labelActionSubmit : {
    type : String ,
    default : 'submit'
  } ,
  typeActionSubmit : {
    type : String ,
    default : 'default'
  } ,
  action : {
    type : Function ,
    default : function ( e )
    {
      console.log( e )
    }
  }


} )

const emits = defineEmits( [ 'close' ] )

</script>

<template>

  <div>

    <div class="modal">

      <div class="modal__header">

        <h5 class="modal__title">
          {{ props.title }}
        </h5>
        <Btn label="×" type="close" style="font-size: 1.5rem;" @click="() => emits('close')"/>

      </div>

      <div class="modal__body">

        <form>

          <slot/>

        </form>

      </div>

      <div class="modal__footer">

        <Btn :type="props.typeActionSubmit" :label="props.labelActionSubmit" @click="props.action"/>

      </div>

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

.modal-section {
  width: 100%;
  position: relative;
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
</style>
