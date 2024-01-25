<template>
  <HeaderComponent />
  <div class="container">
    <IncomeExpenses :income="income" :expenses="expenses" />
    <Balance :total="total" />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import HeaderComponent from './components/HeaderComponent.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref, computed } from 'vue'

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.97 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
])

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
</script>
<style scoped></style>
