<script setup>
import { RouterLink, RouterView } from "vue-router"
import { ref } from 'vue'

const isMobileMenuOpen = ref(false)

function toggleMobileMenu() {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

function closeMobileMenu() {
  isMobileMenuOpen.value = false
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-50 to-blue-50">
    <!-- Header -->
    <header class="sticky top-0 z-50 bg-white shadow-sm border-b border-slate-200 backdrop-blur-sm bg-white/95">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-16">
          <!-- Logo and Brand -->
          <div class="flex items-center space-x-3">
            <div class="w-8 h-8 bg-gradient-to-r from-blue-600 to-indigo-600 rounded-lg flex items-center justify-center">
              <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1"></path>
              </svg>
            </div>
            <h1 class="text-xl font-bold text-slate-800">ResponsibleLend</h1>
          </div>
          
          <!-- Desktop Navigation -->
          <nav class="hidden md:flex space-x-8">
            <RouterLink 
              to="/" 
              class="text-slate-600 hover:text-blue-600 font-medium transition-colors duration-200 px-3 py-2 rounded-md hover:bg-blue-50"
              @click="closeMobileMenu"
            >
              Dashboard
            </RouterLink>
            <RouterLink 
              to="/about" 
              class="text-slate-600 hover:text-blue-600 font-medium transition-colors duration-200 px-3 py-2 rounded-md hover:bg-blue-50"
              @click="closeMobileMenu"
            >
              About
            </RouterLink>
            <RouterLink 
              to="/calculator" 
              class="text-slate-600 hover:text-blue-600 font-medium transition-colors duration-200 px-3 py-2 rounded-md hover:bg-blue-50"
              @click="closeMobileMenu"
            >
              Calculator
            </RouterLink>
          </nav>

          <!-- Mobile menu button -->
          <div class="md:hidden">
            <button
              @click="toggleMobileMenu"
              class="inline-flex items-center justify-center p-2 rounded-md text-slate-600 hover:text-blue-600 hover:bg-blue-50 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-blue-500 transition-colors duration-200"
              :aria-expanded="isMobileMenuOpen"
              aria-label="Toggle navigation menu"
            >
              <!-- Hamburger icon when menu is closed -->
              <svg 
                v-if="!isMobileMenuOpen" 
                class="block h-6 w-6" 
                fill="none" 
                viewBox="0 0 24 24" 
                stroke="currentColor"
              >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
              </svg>
              <!-- X icon when menu is open -->
              <svg 
                v-else 
                class="block h-6 w-6" 
                fill="none" 
                viewBox="0 0 24 24" 
                stroke="currentColor"
              >
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
        </div>

        <!-- Mobile Navigation Menu -->
        <Transition
          enter-active-class="transition ease-out duration-200"
          enter-from-class="opacity-0 scale-95"
          enter-to-class="opacity-100 scale-100"
          leave-active-class="transition ease-in duration-150"
          leave-from-class="opacity-100 scale-100"
          leave-to-class="opacity-0 scale-95"
        >
          <div v-if="isMobileMenuOpen" class="md:hidden">
            <div class="px-2 pt-2 pb-3 space-y-1 bg-white border-t border-slate-200">
              <RouterLink 
                to="/" 
                class="block px-3 py-2 text-base font-medium text-slate-600 hover:text-blue-600 hover:bg-blue-50 rounded-md transition-colors duration-200"
                @click="closeMobileMenu"
              >
                Dashboard
              </RouterLink>
              <RouterLink 
                to="/about" 
                class="block px-3 py-2 text-base font-medium text-slate-600 hover:text-blue-600 hover:bg-blue-50 rounded-md transition-colors duration-200"
                @click="closeMobileMenu"
              >
                About
              </RouterLink>
              <RouterLink 
                to="/calculator" 
                class="block px-3 py-2 text-base font-medium text-slate-600 hover:text-blue-600 hover:bg-blue-50 rounded-md transition-colors duration-200"
                @click="closeMobileMenu"
              >
                Calculator
              </RouterLink>
            </div>
          </div>
        </Transition>
      </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <RouterView />
    </main>

    <!-- Footer -->
    <footer class="bg-slate-800 text-slate-300 mt-16">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <div class="text-center">
          <p class="text-sm">© 2024 ResponsibleLend. Promoting financial wellness through responsible lending practices.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.router-link-active {
  @apply text-blue-600 bg-blue-50;
}

/* Ensure mobile menu appears above other content */
.md\:hidden > div {
  position: relative;
  z-index: 60;
}

/* Smooth backdrop blur effect for sticky header */
header {
  transition: backdrop-filter 0.2s ease-in-out;
}
</style>
