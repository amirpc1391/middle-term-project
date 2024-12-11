<script setup>
import TransactionList from './components/TransactionList.vue'
import Modal from './components/Modal.vue'
import {ref} from "vue";


const isActiveModal = ref(false)

</script>

<template>
  <div class="container">
    <main class="main">
      <TransactionList/>
    </main>
  </div>
  <div :class="{'modal-section': true ,'modal-section--active':isActiveModal}">
    <Modal/>
  </div>
</template>

<style scoped>
.main {
  padding: 15px;
  margin: 15px 0;
  background-color: #2a2f34;
  border-radius: 8px;
}
.modal-section{
  width: 100%;
  position: fixed;
  inset: 0;
  visibility: hidden;
  opacity: 0;
  transition: all .2s ease-in-out;
  background-color: rgba(0, 0, 0, 0.2);
  backdrop-filter: blur(10px);
  padding: 2rem;
}
.modal-section--active{
  visibility: visible;
  opacity: 1;
  padding: 4rem;
}
</style>