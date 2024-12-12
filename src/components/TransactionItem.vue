<script setup>
import Btn from './Btn.vue'
import editIcon from '@/assets/editing.png'
import deleteIcon from '@/assets/delete.png'
import {ref} from "vue"

// color green for income and red for expenses
const colorPrice= ref("red")
</script>

<template>
  <tr class="transaction-section__item">
    <td class="transaction-section__cell">1</td>
    <td class="transaction-section__cell">income</td>
    <td :class="`transaction-section__cell transaction-section__cell--${colorPrice}`">20,000 Toman</td>
    <td class="transaction-section__cell">buy a iceCream</td>
    <td class="transaction-section__cell">
      <div class="transaction-section__cell-btn flex-center">
        <Btn type="edit" label="Edit" :img-icon="editIcon"/>
        <Btn type="delete" label="Delete" :img-icon="deleteIcon"/>
      </div>
    </td>
  </tr>
</template>

<style scoped>
.transaction-section__cell {
  border: 1px solid var(--color_495057);
  padding: 0.75rem;
  font-size: .9rem;
  line-height: 1.4;
}

.transaction-section__cell-btn {
  gap: .3rem;
}
.transaction-section__cell--green{
  color: var(--color_darkgreen);
}
.transaction-section__cell--red{
  color: var(--color_darkred);
}
</style>