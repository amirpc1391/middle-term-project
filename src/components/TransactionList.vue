<script setup>

import TransactionItem from './TransactionItem.vue'
import Btn from "@/components/Btn.vue";
import addIcon from '@/assets/add.png'
import { reactive , ref } from "vue";
import Modal from "@/components/Modal.vue";
import FormInput from "@/components/FormInput.vue";
import Notification from "@/components/Notification.vue";

const props = defineProps( {
  transactions : {
    required : true ,
  }
} )
let isCreate = ref( true )
let editedRecord = ref( -1 )
let isActiveModal = ref( false )
let form = reactive( {
  price : '' ,
  description : ''
} )
let notification = reactive( {
  title : 'successfully' ,
  type : 'success' ,
  active : false ,
  message : ''
} )

let SendNotification = ( message , type = 'success' , title = 'successfully' ) =>
{
  notification.active = true
  notification.message = message
  notification.type = type
  notification.title = title
  setTimeout( () =>
  {
    notification.active = false
  } , 3000 )
}

let createTransaction = () =>
{

  if ( isActiveModal )
  {

    if ( typeof form.price !== 'number' || form.price === 0 )
    {
      SendNotification( 'price is not number!' , 'danger' , 'Warning' )
      return;
    }

    if ( typeof form.description !== 'string' || form.description.length === 0 )
    {
      SendNotification( 'description can not be empty' , 'danger' , 'Warning' )
      return;
    }

    if ( isCreate.value )
    {

      props.transactions.push( {
        count : props.transactions.length + 1 ,
        price : Math.abs( form.price ) ,
        description : form.description ,
        type : form.price < 0 ? 'cost' : 'income'
      } )

      isActiveModal.value = false
      notification.active = false
      form = {
        price : '' ,
        description : ''
      }
      SendNotification( 'Successfully Transaction Added.' )

    } else
    {

      props.transactions[ editedRecord ] = {
        count : props.transactions.length + 1 ,
        price : Math.abs( form.price ) ,
        description : form.description ,
        type : form.price < 0 ? 'cost' : 'income'
      }
      isActiveModal.value = false
      notification.active = false
      isCreate.value = true
      form = {
        price : '' ,
        description : ''
      }
      SendNotification( 'Successfully Transaction Edited.' )

    }

  }

}

let createAction = () =>
{

  isActiveModal.value = true
  isCreate.value = true
  form = {
    price : '' ,
    description : ''
  }

}
let deleteAction = ( e ) =>
{

  if ( confirm( 'Are you sure?' ) )
  {

    let id = e.id
    props.transactions.splice( id , 1 )

  }

}
let editAction = ( e ) =>
{

  let id = e.id
  let transaction = props.transactions[ id ]

  isActiveModal.value = true
  notification.active = false
  form = {
    price : parseInt( transaction.price ) ,
    description : transaction.description
  }
  editedRecord = id
  isCreate.value = false


}

</script>

<template>

  <div class="transaction-section">

    <div class="transaction-section__header">

      <div class="transaction-section__content">
        <img class="transaction-section__img" src="../assets/money.png" alt="money">
        <h1 class="transaction-section__title">list of transactions</h1>
      </div>

      <btn :img-icon="addIcon" type="add" label="Add" @click="createAction"/>

    </div>

    <table class="transaction-section__table">

      <thead class="transaction-section__thead">

      <tr class="transaction-section__row">

        <th class="transaction-section__cell">ID</th>
        <th class="transaction-section__cell">Type of Transaction</th>
        <th class="transaction-section__cell">Price</th>
        <th class="transaction-section__cell">Description</th>
        <th class="transaction-section__cell text-center">Action</th>

      </tr>

      </thead>


      <!--      when exists any transaction-->
      <tbody v-if="true" class="transaction-section__tbody">

      <TransactionItem
          v-for="(item, index) in props.transactions"
          :key="index"
          :id="index"
          :count="item.count"
          :description="item.description"
          :price="item.price"
          :type="item.type"
          @delete="deleteAction"
          @edit="editAction"
      />

      </tbody>

      <!--      when not exists any transaction-->
      <tbody v-else class="transaction-section__tbody">
      <tr class="transaction-section__item">
        <td class="transaction-section__cell-empty" colspan="5">Any transaction no exists ...</td>
      </tr>
      </tbody>

    </table>

  </div>


  <Modal title="Create Transaction" label-action-submit="Create" type-action-submit="add" :action="createTransaction"
         :class="{'modal-section': true ,'modal-section--active':isActiveModal}" @close="isActiveModal = false">

    <form>

      <FormInput id="price" label="price" @change="(e) => form.price = parseInt(e)"/>
      <FormInput id="description" label="description" @change="(e) => form.description = e"/>

    </form>

  </Modal>


  <Notification :title="notification.title" :type="notification.type" @click="notification.active = false"
                :class="{'notification-section':true, 'notification-section--active':notification.active}">
    {{ notification.message }}
  </Notification>

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
  line-height: 1.4;
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

.transaction-section__img {
  width: 1.8rem;
  height: 1.8rem;
}

.transaction-section__cell-empty {
  border: 1px solid var(--color_495057);
  padding: 0.75rem;
  font-size: .9rem;
}


</style>
