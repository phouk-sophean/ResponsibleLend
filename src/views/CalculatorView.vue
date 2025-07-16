<script setup>
import { ref, computed, watch } from 'vue'

const income = ref(null)
const expenses = ref(null)
const requestedAmount = ref(null)
const showResults = ref(false)
const calculationHistory = ref([])

// Computed values
const netIncome = computed(() => {
  if (!income.value || !expenses.value) return 0
  return Math.max(0, income.value - expenses.value)
})

const currentDTI = computed(() => {
  if (!requestedAmount.value || !netIncome.value) return 0
  return (requestedAmount.value / netIncome.value)
})

const maxSafeLoan = computed(() => {
  return netIncome.value * 0.4
})

const riskLevel = computed(() => {
  const dti = currentDTI.value
  if (dti <= 0.2) return { level: 'Low', color: 'green', description: 'Excellent financial position' }
  if (dti <= 0.3) return { level: 'Moderate', color: 'blue', description: 'Good financial position' }
  if (dti <= 0.4) return { level: 'Acceptable', color: 'yellow', description: 'Manageable debt level' }
  return { level: 'High', color: 'red', description: 'High risk of over-indebtedness' }
})

const loanStatus = computed(() => {
  return currentDTI.value <= 0.4 ? 'Likely Approved' : 'Likely Rejected'
})

// Functions
function calculateLoan() {
  if (!income.value || !expenses.value || income.value <= expenses.value) {
    return
  }
  
  showResults.value = true
  
  // Add to calculation history
  calculationHistory.value.unshift({
    id: Date.now(),
    date: new Date().toLocaleDateString(),
    income: income.value,
    expenses: expenses.value,
    netIncome: netIncome.value,
    requestedAmount: requestedAmount.value || 0,
    dti: currentDTI.value,
    maxSafeLoan: maxSafeLoan.value,
    riskLevel: riskLevel.value.level,
    status: loanStatus.value
  })
  
  // Keep only last 5 calculations
  if (calculationHistory.value.length > 5) {
    calculationHistory.value = calculationHistory.value.slice(0, 5)
  }
}

function resetCalculator() {
  income.value = null
  expenses.value = null
  requestedAmount.value = null
  showResults.value = false
}

function formatCurrency(value) {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
  }).format(value)
}

function formatPercentage(value) {
  return (value * 100).toFixed(1) + '%'
}

// Watch for changes to auto-calculate
watch([income, expenses], () => {
  if (income.value && expenses.value && income.value > expenses.value) {
    showResults.value = true
  }
})
</script>

<template>
  <div class="max-w-6xl mx-auto space-y-8">
    <!-- Hero Section -->
    <div class="bg-gradient-to-r from-purple-600 to-indigo-700 rounded-2xl p-8 text-white">
      <div class="max-w-3xl">
        <h1 class="text-3xl font-bold mb-4">Loan Eligibility Calculator</h1>
        <p class="text-purple-100 text-lg leading-relaxed">
          Use our interactive calculator to understand your debt-to-income ratio and determine your maximum safe loan amount before applying. 
          This tool helps you make informed financial decisions and avoid over-indebtedness.
        </p>
      </div>
    </div>

    <div class="grid lg:grid-cols-3 gap-8">
      <!-- Calculator Form -->
      <div class="lg:col-span-2">
        <div class="bg-white rounded-xl shadow-sm border border-slate-200 p-8">
          <div class="flex items-center mb-6">
            <div class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center mr-4">
              <svg class="w-5 h-5 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z"></path>
              </svg>
            </div>
            <div>
              <h2 class="text-2xl font-bold text-slate-800">Financial Calculator</h2>
              <p class="text-slate-600">Enter your financial information to see your loan eligibility</p>
            </div>
          </div>

          <div class="space-y-6">
            <!-- Income and Expenses -->
            <div class="grid md:grid-cols-2 gap-6">
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
                    class="w-full pl-8 pr-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-colors"
                    min="1"
                    step="0.01"
                  />
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
                    class="w-full pl-8 pr-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-colors"
                    min="0"
                    step="0.01"
                  />
                </div>
              </div>
            </div>

            <!-- Requested Loan Amount -->
            <div>
              <label class="block text-sm font-semibold text-slate-700 mb-2">
                Requested Loan Amount (Optional)
              </label>
              <div class="relative">
                <span class="absolute left-3 top-1/2 transform -translate-y-1/2 text-slate-500">$</span>
                <input
                  v-model.number="requestedAmount"
                  type="number"
                  placeholder="50,000"
                  class="w-full pl-8 pr-4 py-3 border border-slate-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-purple-500 transition-colors"
                  min="1"
                  step="0.01"
                />
              </div>
              <p class="text-xs text-slate-500 mt-1">Leave empty to see your maximum safe loan amount</p>
            </div>

            <!-- Action Buttons -->
            <div class="flex gap-4">
              <button 
                @click="calculateLoan"
                :disabled="!income || !expenses || income <= expenses"
                class="flex-1 bg-gradient-to-r from-purple-600 to-indigo-600 text-white font-semibold py-3 px-6 rounded-lg hover:from-purple-700 hover:to-indigo-700 focus:ring-2 focus:ring-purple-500 focus:ring-offset-2 transition-all duration-200 disabled:opacity-50 disabled:cursor-not-allowed"
              >
                Calculate Eligibility
              </button>
              <button 
                @click="resetCalculator"
                class="px-6 py-3 border border-slate-300 text-slate-700 font-semibold rounded-lg hover:bg-slate-50 focus:ring-2 focus:ring-slate-500 focus:ring-offset-2 transition-all duration-200"
              >
                Reset
              </button>
            </div>
          </div>
        </div>

        <!-- Results Section -->
        <div v-if="showResults && netIncome > 0" class="bg-white rounded-xl shadow-sm border border-slate-200 p-8 mt-8">
          <h3 class="text-xl font-bold text-slate-800 mb-6">Calculation Results</h3>
          
          <div class="grid md:grid-cols-2 gap-6 mb-8">
            <!-- Financial Summary -->
            <div class="space-y-4">
              <div class="bg-slate-50 rounded-lg p-4">
                <div class="flex justify-between items-center">
                  <span class="text-sm font-medium text-slate-600">Net Monthly Income</span>
                  <span class="text-lg font-bold text-slate-800">{{ formatCurrency(netIncome) }}</span>
                </div>
              </div>
              
              <div class="bg-blue-50 rounded-lg p-4">
                <div class="flex justify-between items-center">
                  <span class="text-sm font-medium text-blue-700">Maximum Safe Loan</span>
                  <span class="text-lg font-bold text-blue-800">{{ formatCurrency(maxSafeLoan) }}</span>
                </div>
                <p class="text-xs text-blue-600 mt-1">Based on 40% DTI limit</p>
              </div>

              <div v-if="requestedAmount" :class="[
                'rounded-lg p-4',
                currentDTI <= 0.4 ? 'bg-green-50' : 'bg-red-50'
              ]">
                <div class="flex justify-between items-center">
                  <span class="text-sm font-medium" :class="currentDTI <= 0.4 ? 'text-green-700' : 'text-red-700'">
                    Loan Status
                  </span>
                  <span class="text-lg font-bold" :class="currentDTI <= 0.4 ? 'text-green-800' : 'text-red-800'">
                    {{ loanStatus }}
                  </span>
                </div>
              </div>
            </div>

            <!-- DTI Analysis -->
            <div class="space-y-4">
              <div v-if="requestedAmount" class="text-center">
                <div class="relative w-32 h-32 mx-auto mb-4">
                  <svg class="w-32 h-32 transform -rotate-90" viewBox="0 0 36 36">
                    <path
                      d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"
                      fill="none"
                      stroke="#e5e7eb"
                      stroke-width="2"
                    />
                    <path
                      d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"
                      fill="none"
                      :stroke="riskLevel.color === 'green' ? '#10b981' : riskLevel.color === 'blue' ? '#3b82f6' : riskLevel.color === 'yellow' ? '#f59e0b' : '#ef4444'"
                      stroke-width="2"
                      :stroke-dasharray="`${Math.min(currentDTI * 100, 100)}, 100`"
                    />
                  </svg>
                  <div class="absolute inset-0 flex items-center justify-center">
                    <div class="text-center">
                      <div class="text-2xl font-bold text-slate-800">{{ formatPercentage(currentDTI) }}</div>
                      <div class="text-xs text-slate-600">DTI Ratio</div>
                    </div>
                  </div>
                </div>
                
                <div :class="[
                  'inline-flex items-center px-3 py-1 rounded-full text-sm font-medium',
                  riskLevel.color === 'green' ? 'bg-green-100 text-green-800' :
                  riskLevel.color === 'blue' ? 'bg-blue-100 text-blue-800' :
                  riskLevel.color === 'yellow' ? 'bg-yellow-100 text-yellow-800' :
                  'bg-red-100 text-red-800'
                ]">
                  {{ riskLevel.level }} Risk
                </div>
                <p class="text-sm text-slate-600 mt-2">{{ riskLevel.description }}</p>
              </div>

              <div v-else class="text-center py-8">
                <div class="w-16 h-16 bg-purple-100 rounded-full flex items-center justify-center mx-auto mb-4">
                  <svg class="w-8 h-8 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                  </svg>
                </div>
                <p class="text-slate-600">Enter a loan amount to see your DTI analysis</p>
              </div>
            </div>
          </div>

          <!-- Recommendations -->
          <div class="bg-gradient-to-r from-blue-50 to-indigo-50 rounded-lg p-6">
            <h4 class="font-semibold text-slate-800 mb-3">💡 Recommendations</h4>
            <div class="space-y-2 text-sm text-slate-700">
              <div v-if="!requestedAmount || currentDTI <= 0.4" class="flex items-start">
                <svg class="w-4 h-4 text-green-500 mr-2 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                </svg>
                <span>You can safely borrow up to {{ formatCurrency(maxSafeLoan) }} while maintaining healthy finances.</span>
              </div>
              <div v-if="requestedAmount && currentDTI > 0.4" class="flex items-start">
                <svg class="w-4 h-4 text-red-500 mr-2 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L3.732 16.5c-.77.833.192 2.5 1.732 2.5z"></path>
                </svg>
                <span>Consider reducing your loan amount to {{ formatCurrency(maxSafeLoan) }} or increasing your income to improve eligibility.</span>
              </div>
              <div class="flex items-start">
                <svg class="w-4 h-4 text-blue-500 mr-2 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                <span>Keep your debt-to-income ratio below 40% to maintain financial stability and loan approval chances.</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Info Panel -->
      <div class="space-y-6">
        <!-- DTI Guide -->
        <div class="bg-white rounded-xl shadow-sm border border-slate-200 p-6">
          <h3 class="text-lg font-bold text-slate-800 mb-4">DTI Ratio Guide</h3>
          <div class="space-y-3">
            <div class="flex items-center justify-between p-3 bg-green-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">0% - 20%</span>
              <span class="text-sm font-bold text-green-600">Excellent</span>
            </div>
            <div class="flex items-center justify-between p-3 bg-blue-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">20% - 30%</span>
              <span class="text-sm font-bold text-blue-600">Good</span>
            </div>
            <div class="flex items-center justify-between p-3 bg-yellow-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">30% - 40%</span>
              <span class="text-sm font-bold text-yellow-600">Acceptable</span>
            </div>
            <div class="flex items-center justify-between p-3 bg-red-50 rounded-lg">
              <span class="text-sm font-medium text-slate-700">Above 40%</span>
              <span class="text-sm font-bold text-red-600">High Risk</span>
            </div>
          </div>
        </div>

        <!-- Quick Tips -->
        <div class="bg-gradient-to-br from-green-50 to-emerald-50 border border-green-200 rounded-xl p-6">
          <div class="flex items-center mb-3">
            <svg class="w-5 h-5 text-green-600 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"></path>
            </svg>
            <h4 class="font-semibold text-green-800">Pro Tips</h4>
          </div>
          <div class="space-y-2 text-sm text-green-700">
            <p>• Include all sources of monthly income</p>
            <p>• Count all recurring monthly expenses</p>
            <p>• Consider future financial changes</p>
            <p>• Leave room for emergency savings</p>
          </div>
        </div>

        <!-- Calculation History -->
        <div v-if="calculationHistory.length > 0" class="bg-white rounded-xl shadow-sm border border-slate-200 p-6">
          <h3 class="text-lg font-bold text-slate-800 mb-4">Recent Calculations</h3>
          <div class="space-y-3">
            <div 
              v-for="calc in calculationHistory" 
              :key="calc.id"
              class="p-3 bg-slate-50 rounded-lg text-sm"
            >
              <div class="flex justify-between items-center mb-1">
                <span class="font-medium text-slate-700">{{ calc.date }}</span>
                <span :class="[
                  'px-2 py-1 rounded text-xs font-medium',
                  calc.status === 'Likely Approved' ? 'bg-green-100 text-green-700' : 'bg-red-100 text-red-700'
                ]">
                  {{ calc.status }}
                </span>
              </div>
              <div class="text-slate-600">
                <div>Income: {{ formatCurrency(calc.income) }} | Expenses: {{ formatCurrency(calc.expenses) }}</div>
                <div>Max Safe: {{ formatCurrency(calc.maxSafeLoan) }} | DTI: {{ formatPercentage(calc.dti) }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
