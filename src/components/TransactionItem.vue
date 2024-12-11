<script setup>
import Btn from './Btn.vue'
import editIcon from '@/assets/editing.png'
import deleteIcon from '@/assets/delete.png'

</script>

<template>
  <tr class="transaction-section__item">
    <td class="transaction-section__cell">Data</td>
    <td class="transaction-section__cell">Data</td>
    <td class="transaction-section__cell">Data</td>
    <td class="transaction-section__cell">Data</td>
    <td class="transaction-section__cell transaction-section__cell--btn flex-center">
      <Btn type="edit" label="Edit" :img-icon="editIcon"/>
      <Btn type="delete" label="Delete" :img-icon="deleteIcon"/>
    </td>
  </tr>
</template>

<style scoped>
.transaction-section__cell {
  border: 1px solid #495057;
  padding: 0.75rem;
  font-size: .9rem;
}

.transaction-section__cell--btn {
  gap: .3rem;
}
</style>