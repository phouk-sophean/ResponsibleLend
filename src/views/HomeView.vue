<script setup>
import { ref } from 'vue'
import AlertMessage from '../components/AlertMessage.vue'

const loans = ref([])
const amount = ref(null)
const income = ref(null)
const expenses = ref(null)
const alert = ref({ message: '', type: '' })
const isSubmitting = ref(false)

function submitLoan() {
  if (amount.value === null || income.value === null || expenses.value === null) {
    alert.value = { message: 'Please fill all required fields', type: 'error' }
    return
  }

  if (amount.value <= 0 || income.value <= 0 || expenses.value < 0) {
    alert.value = { message: 'Please enter valid positive amounts', type: 'error' }
    return
  }

  if (income.value <= expenses.value) {
    alert.value = { message: 'Monthly expenses cannot be higher than or equal to income', type: 'error' }
    return
  }

  isSubmitting.value = true
  
  // Simulate processing time
  setTimeout(() => {
    const netIncome = income.value - expenses.value
    const dti = amount.value / netIncome
    const status = dti > 0.4 ? 'Rejected (High Risk)' : 'Approved'
    
    loans.value.unshift({
      id: Date.now(),
      amount: amount.value,
      income: income.value,
      expenses: expenses.value,
      netIncome: netIncome,
      dti: dti.toFixed(3),
      status,
      date: new Date().toLocaleDateString(),
    })

    alert.value = {
      message: status === 'Approved' 
        ? 'Congratulations! Your loan application has been approved.' 
        : 'Unfortunately, your loan application was rejected due to high debt-to-income ratio (>40%).',
      type: status === 'Approved' ? 'success' : 'error',
    }

    // Reset form
    amount.value = null
    income.value = null
    expenses.value = null
    isSubmitting.value = false
  }, 1000)
}

function formatCurrency(value) {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
  }).format(value)
}
</script>

<template>
  <div class="space-y-8">
    <!-- Hero Section -->
    <div class="bg-gradient-to-r from-blue-600 to-indigo-700 rounded-2xl p-8 text-white">
      <div class="max-w-3xl">
        <h1 class="text-3xl font-bold mb-4">Responsible Lending Dashboard</h1>
        <p class="text-blue-100 text-lg leading-relaxed">
          Our system promotes financial wellness by ensuring loans are only approved when your debt-to-income ratio stays below 40%. 
          This helps prevent over-indebtedness and supports sustainable financial health.
        </p>
      </div>
    </div>

    <div class="grid lg:grid-cols-3 gap-8">
      <!-- Loan Application Form -->
      <div class="lg:col-span-2">
        <div class="bg-white rounded-xl shadow-sm border border-slate-200 p-8">
          <div class="flex items-center mb-6">
            <div class="w-10 h-10 bg-blue-100 rounded-lg flex items-center justify-center mr-4">
              <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
              </svg>
            </div>
            <div>
              <h2 class="text-2xl font-bold text-slate-800">Loan Application</h2>
              <p class="text-slate-600">Complete the form below to check your eligibility</p>
            </div>
          </div>

          <form @submit.prevent="submitLoan" class="space-y-6">
            <div class="grid md:grid-cols-2 gap-6">
              <div>
                <label class="block text-sm font-semibold text-slate-700 mb-2">
                  Requested Loan Amount *
                </label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-500">$</span>
                  <input
                    v-model.number="amount"
                    type="number"
                    placeholder="50,000"
                    class="w-full pl-8 pr-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-colors"
                    min="1"
                    step="0.01"
                    required
                  />
                </div>
              </div>

              <div>
                <label class="block text-sm font-semibold text-slate-700 mb-2">
                  Monthly Income *
                </label>
                <div class="relative">
                  <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-500">$</span>
                  <input
                    v-model.number="income"
                    type="number"
                    placeholder="5,000"
                    class="w-full pl-8 pr-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-colors"
                    min="1"
                    step="0.01"
                    required
                  />
                </div>
              </div>
            </div>

            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">
                Monthly Expenses *
              </label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-500">$</span>
                <input
                  v-model.number="expenses"
                  type="number"
                  placeholder="3,000"
                  class="w-full pl-8 pr-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-colors"
                  min="0"
                  step="0.01"
                  required
                />
              </div>
            </div>

            <button 
              type="submit" 
              :disabled="isSubmitting"
              class="w-full bg-gradient-to-r from-blue-600 to-indigo-600 text-white font-semibold py-3 px-6 rounded-lg hover:from-blue-700 hover:to-indigo-700 focus:ring-2 focus:ring-blue-500 focus:ring-offset-2 transition-all duration-200 disabled:opacity-50 disabled:cursor-not-allowed flex items-center justify-center"
            >
              <svg v-if="isSubmitting" class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              {{ isSubmitting ? 'Processing...' : 'Submit Application' }}
            </button>
          </form>

          <AlertMessage v-if="alert.message" :message="alert.message" :type="alert.type" class="mt-6" />
        </div>
      </div>

      <!-- Info Panel -->
      <div class="space-y-6">
        <div class="bg-white rounded-xl shadow-sm border border-slate-200 p-6">
          <h3 class="text-lg font-bold text-slate-800 mb-4">Eligibility Criteria</h3>
          <div class="space-y-4">
            <div class="flex items-start">
              <div class="w-2 h-2 bg-green-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
              <div>
                <p class="text-sm font-medium text-slate-700">Debt-to-Income Ratio</p>
                <p class="text-xs text-slate-600">Must be below 40% for approval</p>
              </div>
            </div>
            <div class="flex items-start">
              <div class="w-2 h-2 bg-blue-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
              <div>
                <p class="text-sm font-medium text-slate-700">Positive Net Income</p>
                <p class="text-xs text-slate-600">Income must exceed expenses</p>
              </div>
            </div>
            <div class="flex items-start">
              <div class="w-2 h-2 bg-purple-500 rounded-full mt-2 mr-3 flex-shrink-0"></div>
              <div>
                <p class="text-sm font-medium text-slate-700">Complete Information</p>
                <p class="text-xs text-slate-600">All fields must be filled accurately</p>
              </div>
            </div>
          </div>
        </div>

        <div class="bg-gradient-to-br from-amber-50 to-orange-50 border border-amber-200 rounded-xl p-6">
          <div class="flex items-center mb-3">
            <svg class="w-5 h-5 text-amber-600 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L3.732 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
            </svg>
            <h4 class="font-semibold text-amber-800">Important Notice</h4>
          </div>
          <p class="text-sm text-amber-700">
            This system is designed to protect borrowers from over-indebtedness. A debt-to-income ratio above 40% indicates potential financial stress.
          </p>
        </div>
      </div>
    </div>

    <!-- Applications History -->
    <div class="bg-white rounded-xl shadow-sm border border-slate-200">
      <div class="p-6 border-b border-slate-200">
        <div class="flex items-center justify-between">
          <div>
            <h2 class="text-xl font-bold text-slate-800">Application History</h2>
            <p class="text-slate-600">Track your loan applications and their status</p>
          </div>
          <div class="bg-slate-100 px-3 py-1 rounded-full">
            <span class="text-sm font-medium text-slate-700">{{ loans.length }} Applications</span>
          </div>
        </div>
      </div>

      <div class="overflow-x-auto">
        <table class="w-full">
          <thead class="bg-slate-50">
            <tr>
              <th class="text-left py-4 px-6 font-semibold text-slate-700">Date</th>
              <th class="text-left py-4 px-6 font-semibold text-slate-700">Amount</th>
              <th class="text-left py-4 px-6 font-semibold text-slate-700">Income</th>
              <th class="text-left py-4 px-6 font-semibold text-slate-700">Expenses</th>
              <th class="text-left py-4 px-6 font-semibold text-slate-700">Net Income</th>
              <th class="text-left py-4 px-6 font-semibold text-slate-700">DTI Ratio</th>
              <th class="text-left py-4 px-6 font-semibold text-slate-700">Status</th>
            </tr>
          </thead>
          <tbody class="divide-y divide-slate-200">
            <tr v-for="loan in loans" :key="loan.id" class="hover:bg-slate-50 transition-colors">
              <td class="py-4 px-6 text-sm text-slate-600">{{ loan.date }}</td>
              <td class="py-4 px-6 text-sm font-medium text-slate-900">{{ formatCurrency(loan.amount) }}</td>
              <td class="py-4 px-6 text-sm text-slate-600">{{ formatCurrency(loan.income) }}</td>
              <td class="py-4 px-6 text-sm text-slate-600">{{ formatCurrency(loan.expenses) }}</td>
              <td class="py-4 px-6 text-sm text-slate-600">{{ formatCurrency(loan.netIncome) }}</td>
              <td class="py-4 px-6 text-sm font-mono">{{ (loan.dti * 100).toFixed(1) }}%</td>
              <td class="py-4 px-6">
                <span 
                  :class="[
                    'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium',
                    loan.status.includes('Rejected') 
                      ? 'bg-red-100 text-red-800' 
                      : 'bg-green-100 text-green-800'
                  ]"
                >
                  {{ loan.status }}
                </span>
              </td>
            </tr>
            <tr v-if="loans.length === 0">
              <td colspan="7" class="text-center py-12">
                <div class="flex flex-col items-center">
                  <svg class="w-12 h-12 text-slate-400 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                  </svg>
                  <p class="text-slate-500 font-medium">No loan applications yet</p>
                  <p class="text-slate-400 text-sm">Submit your first application above to get started</p>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>