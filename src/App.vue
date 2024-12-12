<script setup>
import TransactionList from './components/TransactionList.vue'
import Modal from './components/Modal.vue'
import Notification from './components/Notification.vue'
import {ref} from "vue";


const isActiveModal = ref(false)
const isActiveNotification = ref(false)

</script>

<template>
  <div class="container">
    <div class="main">
      <TransactionList/>
    </div>
    <div class="report-section">
      <div class="report-section__balance"><span class="report-section__balance-title">Total Balance: </span>500,000 Toman</div>
      <div class="report-section__incomes"><span class="report-section__incomes-title">Total Incomes: </span>1,500,000 Toman</div>
      <div class="report-section__expenses"><span class="report-section__expenses-title">Total Expenses: </span>-1,000,000 Toman</div>
    </div>
  </div>

  <div :class="{'modal-section': true ,'modal-section--active':isActiveModal}">
    <Modal/>
  </div>

  <div :class="{'notification-section':true, 'notification-section--active':isActiveNotification}">
<!--    for type props in Notification you can use danger , success , notice-->
    <Notification  title="success" type="success">
      Budget Tracker app loaded.<br> You can add your first transaction.
    </Notification>
  </div>

</template>

<style scoped>
.main {
  padding: 15px;
  margin: 15px 0;
  background-color: var(--color_2a2f34);
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
  padding: 3rem;
}
.modal-section--active{
  visibility: visible;
  opacity: 1;
  padding: 5rem;
}
.report-section{
  //display: flex;
  //background-color: var(--color_2a2f34);
  //border-radius: 8px;
  //color: var(--color_dee2e6);
  //padding: 1.25rem;
  //justify-content: space-between;
  //align-items: center;

  display: grid;
  justify-items: flex-start;
  grid-template-columns: repeat(3, 1fr);
  gap: .8rem .2rem;
  background-color: var(--color_2a2f34);
  border-radius: 8px;
  color: var(--color_dee2e6);
  padding: 1.25rem;
}
.report-section__incomes,.report-section__expenses,.report-section__balance{
display: flex;
  gap: .5rem;
  justify-content: center;
  align-items: baseline;
}

.report-section__balance-title,.report-section__incomes-title,.report-section__expenses-title{
  font-weight: 500;
  font-size: 1.2rem;
}
.report-section__balance-title{
  color: var(--color_1791ba);
}
.report-section__incomes-title{
  color: var(--color_darkgreen);
}
.report-section__expenses-title{
  color: var(--color_darkred);
}
.notification-section{
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  gap: 1rem;
  align-items: center;
  width: 100%;
  position: fixed;
  inset: 0;
  visibility: hidden;
  opacity: 0;
  transition: all .2s ease-in-out;
  padding: .6rem;
}
.notification-section--active{
  visibility: visible;
  opacity: 1;
}
</style>