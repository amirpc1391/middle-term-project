<script setup>
import TransactionList from './components/TransactionList.vue'
import Modal from './components/Modal.vue'
import Notification from './components/Notification.vue'
import {computed, onMounted, reactive, watch, ref} from "vue";


const isActiveModal = ref(false)
const modalStatusEdit = ref(false)
const editCorrentTransactionIndex = ref(-1)
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
const notification = reactive({
  title: '',
  type: '',
  isActive: false,
  message: ''
})
const inputsValue = ref({
  price: 0,
  description: ''
})

const SendNotification = (message, type = 'success', title = 'successfully') => {
  notification.isActive = true
  notification.message = message
  notification.type = type
  notification.title = title
  setTimeout(() => {
    notification.isActive = false
  }, 1000)
}
onMounted(() => {
  SendNotification(`Budget Tracker app loaded.You can add your first transaction.`, 'success', "successfully")
})

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
watch(calculateReport, () => {
  if (calculateReport.value.balance < 0) {
    console.log('Warning Balance!')
    SendNotification(`Warning Balance!.`, 'notice', "notice")
  }
})

const modalAddTransaction = () => {
  isActiveModal.value = true
  modalStatusEdit.value = false
  console.log("modalAddTransaction")
}
const modalEditTransaction = (index) => {
  isActiveModal.value = true
  modalStatusEdit.value = true
  editCorrentTransactionIndex.value = index
  inputsValue.value.price = transactionsList.value[index].price;
  inputsValue.value.description = transactionsList.value[index].description;
  console.log("modalEditTransaction")
}
const modalDeleteTransaction = (index) => {
  console.log("modalDeleteTransaction")
  transactionsList.value.splice(index, 1)
}
const submitModal = () => {
  if (!isNaN(inputsValue.value.price) && inputsValue.value.price && inputsValue.value.description) {

    if (modalStatusEdit.value) {
      if (editCorrentTransactionIndex.value < 0) {
        SendNotification("edit transaction Error , index item invalid", 'danger', 'Error')
      } else {
        transactionsList.value[editCorrentTransactionIndex.value].price = +inputsValue.value.price
        transactionsList.value[editCorrentTransactionIndex.value].description = inputsValue.value.description
        SendNotification("transaction edited", 'success', 'successfully')
      }
    } else {
      transactionsList.value.push({
        description: inputsValue.value.description,
        price: +inputsValue.value.price
      })
      SendNotification("transaction edited", 'success', 'successfully')
    }
    inputsValue.value.price = 0
    inputsValue.value.description = ""
    modalStatusEdit.value = false
    isActiveModal.value = false
    editCorrentTransactionIndex.value = -1
  } else {
    SendNotification("invalid inputs value , plz enter inputs valid value for inputs", 'danger', 'Error')
  }
  console.log("submitted")
}
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
  <Modal :is-active-modal="isActiveModal" :modalStatusEdit="modalStatusEdit" @modal-close="closeModal" @modal-submit="submitModal"
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