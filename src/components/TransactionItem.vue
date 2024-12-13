<script setup>
import Btn from './Btn.vue'
import editIcon from '@/assets/editing.png'
import deleteIcon from '@/assets/delete.png'
import { onMounted , ref } from "vue"

// color green for income and red for expenses
const colorPrice = ref( "red" )

const props = defineProps( {

  id : {
    required : true ,
    type : Number
  } ,
  count : {
    type : Number ,
    required : true
  } ,
  type : {
    type : String ,
    required : true
  } ,
  price : {
    type : Number ,
    required : true
  } ,
  description : {
    type : String ,
    required : true
  }

} );

onMounted( () =>
{

  if ( props.type === 'income' )
  {
    colorPrice.value = 'green';
  }

} )

const emits = defineEmits( [ 'delete' , 'edit' ] )

</script>

<template>
  <tr class="transaction-section__item">
    <td class="transaction-section__cell">
      {{ props.count }}
    </td>
    <td class="transaction-section__cell">
      {{ props.type }}
    </td>
    <td :class="`transaction-section__cell transaction-section__cell--${colorPrice}`">
      {{ props.price.toLocaleString() }}
      Toman
    </td>
    <td class="transaction-section__cell">
      {{ props.description }}
    </td>
    <td class="transaction-section__cell">
      <div class="transaction-section__cell-btn flex-center">
        <Btn type="edit" label="Edit" :img-icon="editIcon" @click="() => emits('edit',{id:id})"/>
        <Btn type="delete" label="Delete" :img-icon="deleteIcon" @click="() => emits('delete',{id:props.id})"/>
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

.transaction-section__cell--green {
  color: var(--color_darkgreen);
}

.transaction-section__cell--red {
  color: var(--color_darkred);
}
</style>
