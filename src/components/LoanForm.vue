<template>
  <div class="p-4 bg-white shadow rounded mb-4">
    <h2 class="text-lg font-semibold mb-2">Loan Application</h2>
    <form @submit.prevent="submitLoan">
      <input v-model.number="amount" type="number" placeholder="Loan Amount" class="input" />
      <input v-model.number="income" type="number" placeholder="Monthly Income" class="input" />
      <input v-model.number="expenses" type="number" placeholder="Monthly Expenses" class="input" />
      <button class="btn mt-2">Submit</button>
    </form>
    <AlertMessage v-if="message" :message="message" :type="alertType" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import AlertMessage from './AlertMessage.vue'

const amount = ref()
const income = ref()
const expenses = ref()
const message = ref("")
const alertType = ref("info")

function submitLoan() {
  const netIncome = income.value - expenses.value
  const debtRatio = amount.value / netIncome

  if (debtRatio > 0.4) {
    message.value = "❌ Loan rejected: Over-indebted"
    alertType.value = "error"
  } else {
    message.value = "✅ Loan approved"
    alertType.value = "success"
  }
}
</script>

<style scoped>
.input {
  display: block;
  width: 100%;
  padding: 10px 12px;
  margin: 12px 0;
  font-size: 1rem;
  border: 1.5px solid #cbd5e1; /* Tailwind slate-300 */
  border-radius: 0.375rem; /* rounded-md */
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}

.input:focus {
  outline: none;
  border-color: #3b82f6; /* Tailwind blue-500 */
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.3);
}

.btn {
  padding: 12px 24px;
  background-color: #2563eb; /* Tailwind blue-600 */
  color: white;
  font-weight: 600;
  border: none;
  border-radius: 0.375rem; /* rounded-md */
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-size: 1rem;
  box-shadow: 0 2px 8px rgb(37 99 235 / 0.4);
}

.btn:hover {
  background-color: #1d4ed8; /* Tailwind blue-700 */
  box-shadow: 0 4px 12px rgb(29 78 216 / 0.6);
}

.btn:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.6);
}
</style>
