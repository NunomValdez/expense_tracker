<template>
  <HeaderComponent />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <TransactionList />
    <AddTransaction />
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

export default {
  components: {
    HeaderComponent,
    Balance,
    IncomeExpenses,
    TransactionList,
    AddTransaction
  }
}
</script>
<style scoped></style>
