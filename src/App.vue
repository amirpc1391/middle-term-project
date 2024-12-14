<script setup>
import TransactionList from './components/TransactionList.vue'
import Modal from './components/Modal.vue'
import Notification from './components/Notification.vue'
import {computed, onMounted, reactive, watch, ref} from "vue";

// Show or hide the Modal
const isActiveModal = ref(false)
// Specify the modal mode (true for editing a transaction mode and false for creating a transaction mode)
const modalStatusEdit = ref(false)
// Specify the index of the transaction that is being edited
const editCorrentTransactionIndex = ref(-1)
//transaction list
const transactionsList = ref([
  {
    description: "ice-cream",
    price: 10000
  },
  {
    description: "1ice-cream",
    price: 20000
  },
  {
    description: "2ice-cream",
    price: 30000
  },
  {
    description: "3ice-cream",
    price: 40000
  }
])
//notification values
const notification = reactive({
  title: '',
  type: '',
  isActive: false,
  message: ''
})
//inputs values(connected with v-model)
const inputsValue = ref({
  price: 0,
  description: ''
})
//function for show Notification and hide it after 1 second with specified message and type
const SendNotification = (message, type = 'success', title = 'successfully') => {
  notification.isActive = true
  notification.message = message
  notification.type = type
  notification.title = title
  setTimeout(() => {
    notification.isActive = false
  }, 1000)
}
//show notification when the app is loaded
onMounted(() => {
  SendNotification(`Budget Tracker app loaded.You can add your first transaction.`, 'success', "successfully")
})
//computed for calculate report values (balance , incomes , expenses)
const calculateReport = computed(() => {
  let expenses = 0;
  let incomes = 0;
  if (transactionsList.value.length > 0) {
    let transaction = {}
    for (let i = 0; i < transactionsList.value.length; i++) {
      transaction = transactionsList.value[i]
      if (transaction.price > 0) {
        incomes += transaction.price;
      } else {
        expenses += transaction.price;
      }
    }
  }
  return {
    balance: incomes + expenses,
    incomes,
    expenses
  };

})
//watch for calculateReport ,show warning when balance is negative
watch(calculateReport, () => {
  if (calculateReport.value.balance < 0) {
    console.log('Warning Balance!')
    SendNotification(`Warning Balance!.`, 'notice', "notice")
  }
})
//onClick event function for Add Transaction button
const modalAddTransaction = () => {
  isActiveModal.value = true
  modalStatusEdit.value = false
  inputsValue.value.price = 0
  inputsValue.value.description = ""
  console.log("modalAddTransaction")
}
//onClick event function for Edit Transaction button
const modalEditTransaction = (index) => {
  isActiveModal.value = true
  modalStatusEdit.value = true
  editCorrentTransactionIndex.value = index
  inputsValue.value.price = transactionsList.value[index].price;
  inputsValue.value.description = transactionsList.value[index].description;
  console.log("modalEditTransaction")
}
//onClick event function for Delete Transaction button
const modalDeleteTransaction = (index) => {
  console.log("modalDeleteTransaction")
  transactionsList.value.splice(index, 1)
  SendNotification("Transaction deleted", 'success', 'successfully')
}
//onClick event function for Submit Modal button (Add or Edit)
const submitModal = () => {
  //validate inputs of modal
  if (!isNaN(inputsValue.value.price) && inputsValue.value.price && inputsValue.value.description) {
    //check for edit or add
    if (modalStatusEdit.value) {
      //check for valid index
      if (editCorrentTransactionIndex.value < 0) {
        SendNotification("Edit transaction Error , Index item invalid", 'danger', 'Error')
      } else {
        transactionsList.value[editCorrentTransactionIndex.value].price = +inputsValue.value.price
        transactionsList.value[editCorrentTransactionIndex.value].description = inputsValue.value.description
        SendNotification("Transaction edited", 'success', 'successfully')
      }
    } else {
      transactionsList.value.push({
        description: inputsValue.value.description,
        price: +inputsValue.value.price
      })
      SendNotification("Transaction added to list", 'success', 'successfully')
    }
    //reset values of inputs and ...
    inputsValue.value.price = 0
    inputsValue.value.description = ""
    modalStatusEdit.value = false
    isActiveModal.value = false
    editCorrentTransactionIndex.value = -1
  } else {
    SendNotification("Invalid inputs value , Please enter inputs valid value for inputs", 'danger', 'Error')
  }
  console.log("submitted")
}
//onClick event function for Close Modal button
const closeModal = () => {
  isActiveModal.value = false
  console.log("closeModal")
}
</script>

<template>
  <div class="container">
    <div class="main">
      <TransactionList :transactionsList="transactionsList" @modal-add-transaction="modalAddTransaction"
                       @modal-edit-transaction="modalEditTransaction"
                       @modal-delete-transaction="modalDeleteTransaction"/>
    </div>
    <div class="report-section">
      <div class="report-section__balance"><span
          class="report-section__balance-title">Total Balance: </span>{{ calculateReport.balance.toLocaleString() }}
        Toman
      </div>
      <div class="report-section__incomes"><span
          class="report-section__incomes-title">Total Incomes: </span>{{ calculateReport.incomes.toLocaleString() }}
        Toman
      </div>
      <div class="report-section__expenses"><span
          class="report-section__expenses-title">Total Expenses: </span>{{ calculateReport.expenses.toLocaleString() }}
        Toman
      </div>
    </div>
  </div>
  <Modal :is-active-modal="isActiveModal" :modalStatusEdit="modalStatusEdit" @modal-close="closeModal"
         @modal-submit="submitModal"
         v-model:price="inputsValue.price" v-model:description="inputsValue.description"/>

  <!--    for type props in Notification you can use danger , success , notice-->
  <Notification :title="notification.title" :type="notification.type" :is-active-notification="notification.isActive">
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