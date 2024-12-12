<script setup>
import TransactionItem from './TransactionItem.vue'
import Btn from "@/components/Btn.vue";
import addIcon from '@/assets/add.png'
</script>

<template>
  <div class="transaction-section">

    <div class="transaction-section__header">
      <div class="transaction-section__content">
        <img class="transaction-section__img" src="../assets/money.png" alt="money">
        <h1 class="transaction-section__title">list of transactions</h1>
      </div>
      <btn :img-icon="addIcon" type="add" label="Add"/>
    </div>
    <table class="transaction-section__table">
      <thead class="transaction-section__thead">
      <tr class="transaction-section__row">
        <th class="transaction-section__cell">Number</th>
        <th class="transaction-section__cell">Type of Transaction</th>
        <th class="transaction-section__cell">Price</th>
        <th class="transaction-section__cell">Description</th>
        <th class="transaction-section__cell text-center">Action</th>
      </tr>
      </thead>
<!--      when exists any transaction-->
      <tbody v-if="true" class="transaction-section__tbody">
      <TransactionItem/>
      <TransactionItem/>
      <TransactionItem/>
      <TransactionItem/>
      <TransactionItem/>
      <TransactionItem/>
      </tbody>
      <!--      when not exists any transaction-->
      <tbody v-else class="transaction-section__tbody">
      <tr class="transaction-section__item">
        <td class="transaction-section__cell-empty" colspan="5">Any transaction no exists ...</td>
      </tr>
      </tbody>

    </table>
  </div>
</template>


<style scoped>

.transaction-section {
  background-color: var(--color_212529);
}

.transaction-section__table {
  color: var(--color_dee2e6);
  width: 100%;
  border-collapse: collapse;
  border: 1px solid var(--color_2a2f34);
  text-align: center;
}

.transaction-section__cell {
  border: 1px solid var(--color_495057);
  padding: 0.75rem;
  font-size: 0.9rem;
}

.transaction-section__thead th {
  vertical-align: bottom;
  border-bottom: 2px solid var(--color_495057);
}

.transaction-section__tbody tr:hover {
  color: var(--color_adb5bd);
  background-color: rgba(0, 0, 0, 0.075);
}

.transaction-section__header {
  padding: 1rem;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  border: 1px solid var(--color_495057);
}

.transaction-section__content {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: .5rem;
}

.transaction-section__title {
  color: var(--color_1791ba);
  text-transform: capitalize;
  font-size: 1.5rem;
}
.transaction-section__img{
  width: 1.8rem;
  height: 1.8rem;
}

.transaction-section__cell-empty{
  border: 1px solid var(--color_495057);
  padding: 0.75rem;
  font-size: .9rem;
}

</style>