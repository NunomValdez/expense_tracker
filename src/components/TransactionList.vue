<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }}
      <span>{{ transaction.amount }}€</span>
      <button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from 'vue'

// in order to use props, we need to define it in the component, so it knows what to expect
const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})
</script>
