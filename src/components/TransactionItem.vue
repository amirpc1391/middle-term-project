<script setup>
import Btn from './Btn.vue'
import editIcon from '@/assets/editing.png'
import deleteIcon from '@/assets/delete.png'
import {computed, ref} from "vue"

const props=defineProps({
  transactionItem: {
    type: Object,
    required: true
  }
})
// color green for income and red for expenses
const colorPriceComputed=computed(()=>{
  if (props.transactionItem.price>=0){
    return "green"
  }else {
    return "red"
  }
})
</script>

<template>
  <tr class="transaction-section__item">
    <td class="transaction-section__cell">{{transactionItem.id}}</td>
    <td v-if="transactionItem.price>=0" class="transaction-section__cell">income</td>
    <td v-else class="transaction-section__cell">expense</td>
    <td :class="`transaction-section__cell transaction-section__cell--${colorPriceComputed}`">{{transactionItem.price.toLocaleString()}} Toman</td>
    <td class="transaction-section__cell">{{transactionItem.description}}</td>
    <td class="transaction-section__cell">
      <div class="transaction-section__cell-btn flex-center">
        <Btn type="edit" label="Edit" :img-icon="editIcon" @click-btn="$emit('edit-btn')"/>
        <Btn type="delete" label="Delete" :img-icon="deleteIcon" @click-btn="$emit('delete-btn')"/>
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