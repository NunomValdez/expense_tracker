<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <h3>Add new Transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amout"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input type="text" v-model="amount" id="amount" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add Transaction</button>
  </form>
</template>

<script setup>
import { ref, defineEmits } from 'vue'
import { useToast } from 'vue-toastification'

const emit = defineEmits(['transactionSubmitted'])

const text = ref('')
const amount = ref('')
const toast = useToast()

const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled')
    return
  }
  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }

  emit('transactionSubmitted', transactionData)

  text.value = ''
  amount.value = ''
}
</script>
