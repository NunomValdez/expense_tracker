<template>
  <HeaderComponent />
  <div class="container">
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <Balance :total="+total" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleDeleteTransaction" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>

<script setup>
import HeaderComponent from './components/HeaderComponent.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref, computed, onMounted } from 'vue'
import { useToast } from 'vue-toastification'

const toast = useToast()
const transactions = ref([])

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
  if (savedTransactions) {
    transactions.value = savedTransactions
  }
})

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
  //we need to use the .value, because we're using the ref from vue
})

// Get Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => {
      return transaction.amount > 0
    })
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})
//Get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => {
      return transaction.amount < 0
    })
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

//Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })
  saveTransactionsToLocalStorage()
  toast.success('Transaction added')
}

// Generate Unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000)
}

//Delete transaction
const handleDeleteTransaction = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)
  saveTransactionsToLocalStorage()
  toast.success('Transaction Deleted')
}

// Save to localStorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>
<style scoped></style>
