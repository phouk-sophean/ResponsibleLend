<script setup>
import { computed, defineProps, onMounted, ref } from 'vue'

const props = defineProps({
  message: String,
  type: {
    type: String,
    default: 'info', // 'success' | 'error' | 'info' | 'warning'
  },
})

const isVisible = ref(true)

const alertConfig = computed(() => {
  const configs = {
    success: {
      bgColor: 'bg-green-50',
      borderColor: 'border-green-200',
      textColor: 'text-green-800',
      iconColor: 'text-green-500',
      icon: 'M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z'
    },
    error: {
      bgColor: 'bg-red-50',
      borderColor: 'border-red-200',
      textColor: 'text-red-800',
      iconColor: 'text-red-500',
      icon: 'M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L3.732 16.5c-.77.833.192 2.5 1.732 2.5z'
    },
    info: {
      bgColor: 'bg-blue-50',
      borderColor: 'border-blue-200',
      textColor: 'text-blue-800',
      iconColor: 'text-blue-500',
      icon: 'M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z'
    },
    warning: {
      bgColor: 'bg-amber-50',
      borderColor: 'border-amber-200',
      textColor: 'text-amber-800',
      iconColor: 'text-amber-500',
      icon: 'M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-2.5L13.732 4c-.77-.833-1.964-.833-2.732 0L3.732 16.5c-.77.833.192 2.5 1.732 2.5z'
    }
  }
  return configs[props.type] || configs.info
})

function dismiss() {
  isVisible.value = false
}

// Auto-dismiss after 5 seconds for success messages
onMounted(() => {
  if (props.type === 'success') {
    setTimeout(() => {
      isVisible.value = false
    }, 5000)
  }
})
</script>

<template>
  <Transition
    enter-active-class="transition ease-out duration-300"
    enter-from-class="opacity-0 transform scale-95"
    enter-to-class="opacity-100 transform scale-100"
    leave-active-class="transition ease-in duration-200"
    leave-from-class="opacity-100 transform scale-100"
    leave-to-class="opacity-0 transform scale-95"
  >
    <div 
      v-if="isVisible"
      :class="[
        alertConfig.bgColor,
        alertConfig.borderColor,
        alertConfig.textColor,
        'border rounded-lg p-4 flex items-start space-x-3'
      ]"
    >
      <svg 
        :class="[alertConfig.iconColor, 'w-5 h-5 flex-shrink-0 mt-0.5']" 
        fill="none" 
        stroke="currentColor" 
        viewBox="0 0 24 24"
      >
        <path 
          stroke-linecap="round" 
          stroke-linejoin="round" 
          stroke-width="2" 
          :d="alertConfig.icon"
        />
      </svg>
      
      <div class="flex-1">
        <p class="text-sm font-medium leading-relaxed">{{ message }}</p>
      </div>
      
      <button 
        @click="dismiss"
        :class="[alertConfig.iconColor, 'hover:opacity-75 transition-opacity']"
        class="flex-shrink-0"
      >
        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>
  </Transition>
</template>