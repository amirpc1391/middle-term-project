<script setup>
import TransactionList from './components/TransactionList.vue'
import transactions_saves from "@/transactions.json";
import { computed , onMounted , reactive , watch } from "vue";
import Notification from "@/components/Notification.vue";

let transactions = reactive( transactions_saves )
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

const calculator = computed( () =>
{
  let Balance = 0;
  let Incomes = 0;
  let Expenses = 0;

  if ( transactions.length > 0 )
  {

    for ( let i = 0 ; i < transactions.length ; i++ )
    {

      let transaction = transactions[ i ]

      if ( transaction.type === 'income' )
      {
        Balance += transactions[ i ].price;
      }
      if ( transaction.type === 'cost' )
      {
        Incomes += transactions[ i ].price;
      }

    }

    Expenses = Balance - Incomes

  }

  return {
    Balance : Balance ,
    Incomes : Incomes ,
    Expenses : Expenses
  };

} )

watch( calculator , () =>
{

  if ( calculator.value.Expenses < 0 )
  {
    console.log( 'Warning Balance!' )
  }

} )

onMounted( () =>
{

  // console.log( 'برنامه ردیابی بودجه بارگزاری شد.' )
  SendNotification( 'برنامه ردیابی بودجه بارگزاری شد.' )

} )

</script>

<template>
  <div class="container">

    <div class="main">
      <TransactionList :transactions="transactions"/>
    </div>

    <div class="report-section" @click="isActiveNotification=true">
      <div class="report-section__balance"><span class="report-section__balance-title">
        Total Balance:
      </span>
        {{ calculator.Balance.toLocaleString() }}
        Toman
      </div>
      <div class="report-section__incomes"><span class="report-section__incomes-title">
        Total Incomes:
      </span>
        {{ calculator.Incomes.toLocaleString() }}
        Toman
      </div>
      <div class="report-section__expenses"><span class="report-section__expenses-title">
        Total Expenses:
      </span>
        {{ calculator.Expenses.toLocaleString() }}
        Toman
      </div>
    </div>
  </div>

  <Notification :title="notification.title" :type="notification.type" @click="notification.active = false"
                :class="{'notification-section':true, 'notification-section--active':notification.active}">
    {{ notification.message }}
  </Notification>

</template>

<style scoped>
.main {
  padding: 15px;
  margin: 15px 0;
  background-color: var(--color_2a2f34);
  border-radius: 8px;
}


.report-section {
  display: grid;
  justify-items: flex-start;
  grid-template-columns: repeat(3, 1fr);
  gap: .8rem .2rem;
  background-color: var(--color_2a2f34);
  border-radius: 8px;
  color: var(--color_dee2e6);
  padding: 1.25rem;
}

.report-section__incomes, .report-section__expenses, .report-section__balance {
  display: flex;
  gap: .5rem;
  justify-content: center;
  align-items: baseline;
}

.report-section__balance-title, .report-section__incomes-title, .report-section__expenses-title {
  font-weight: 500;
  font-size: 1.2rem;
}

.report-section__balance-title {
  color: var(--color_1791ba);
}

.report-section__incomes-title {
  color: var(--color_darkgreen);
}

.report-section__expenses-title {
  color: var(--color_darkred);
}


</style>
