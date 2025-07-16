<template>
  <div class="p-4">
    <h2 class="text-lg font-bold">Loan Applications</h2>
    <ul>
      <li v-for="loan in loans" :key="loan.id">
        ${{ loan.amount }} - Status: <span :class="loan.status">{{ loan.status }}</span>
      </li>
    </ul>
  </div>
</template>

<script setup>
const loans = [
  { id: 1, amount: 500, status: 'approved' },
  { id: 2, amount: 2000, status: 'rejected' },
]
</script>
