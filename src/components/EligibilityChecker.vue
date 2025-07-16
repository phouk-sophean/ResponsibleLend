<template>
  <div class="p-4 bg-white shadow rounded">
    <h2 class="text-lg font-semibold mb-2">Check Your Eligibility</h2>
    <input v-model.number="income" type="number" placeholder="Monthly Income" class="input" />
    <input v-model.number="expenses" type="number" placeholder="Monthly Expenses" class="input" />
    <button class="btn mt-2" @click="checkEligibility">Check</button>
    <p v-if="result" class="mt-2 font-medium">{{ result }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const income = ref()
const expenses = ref()
const result = ref("")

function checkEligibility() {
  const net = income.value - expenses.value
  const maxLoan = net * 0.4
  result.value = `✅ You can safely borrow up to $${maxLoan.toFixed(2)}`
}
</script>

<style scoped>
.input {
  display: block;
  margin: 10px 0;
  padding: 8px;
  border: 1px solid #ccc;
  width: 100%;
}
.btn {
  padding: 8px 16px;
  background-color: #22c55e;
  color: white;
  border: none;
  border-radius: 4px;
}
</style>