<script setup lang="ts">
import { ref } from 'vue'
import { RouterLink, useRoute } from 'vue-router'

const isMenuOpen = ref(false)
const route = useRoute()

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}
</script>

<template>
  <nav class="bg-green-600 shadow-lg relative z-50">
    <div class="container mx-auto px-4">
      <!-- Barre de navigation principale -->
      <div class="flex justify-between items-center h-16">
        <RouterLink 
          to="/" 
          class="text-white font-bold text-xl hover:text-blue-200 transition-colors duration-300"
        >
          Logo
        </RouterLink>

        <!-- Menu Desktop -->
        <div class="hidden md:flex space-x-1">
          <RouterLink 
            v-for="link in [
              { to: '/', text: 'Accueil' },
              { to: '/about', text: 'À propos' },
              { to: '/contact', text: 'Contact' }
            ]" 
            :key="link.to"
            :to="link.to"
            class="relative text-white px-3 py-2 rounded-md transition-all duration-300 group"
            :class="{ 'font-medium': route.path === link.to }"
          >
            <span>{{ link.text }}</span>
            <span 
              class="absolute bottom-0 left-0 right-0 h-0.5 bg-white transition-all duration-300 transform scale-x-0 group-hover:scale-x-100"
              :class="{ 'scale-x-100': route.path === link.to }"
            ></span>
          </RouterLink>
        </div>

        <!-- Bouton Mobile -->
        <button 
          @click="toggleMenu"
          class="md:hidden text-white focus:outline-none p-2 transition-transform duration-300"
          :class="{ 'rotate-180': isMenuOpen }"
          aria-label="Menu"
        >
          <svg 
            class="h-6 w-6 transition-all duration-300"
            fill="none" 
            viewBox="0 0 24 24" 
            stroke="currentColor"
          >
            <path 
              stroke-linecap="round" 
              stroke-linejoin="round" 
              stroke-width="2" 
              :d="isMenuOpen ? 'M6 18L18 6M6 6l12 12' : 'M4 6h16M4 12h16M4 18h16'"
            />
          </svg>
        </button>
      </div>

      <!-- Overlay avec fondu -->
      <transition name="fade">
        <div 
          v-if="isMenuOpen"
          @click="toggleMenu"
          class="fixed inset-0 bg-black bg-opacity-50 z-40 md:hidden"
          style="margin-top: 4rem;"
        ></div>
      </transition>

      <!-- Menu Mobile avec animation slide-down -->
      <transition
        enter-active-class="transition-all duration-300 ease-out"
        enter-from-class="opacity-0 -translate-y-4"
        enter-to-class="opacity-100 translate-y-0"
        leave-active-class="transition-all duration-200 ease-in"
        leave-from-class="opacity-100 translate-y-0"
        leave-to-class="opacity-0 -translate-y-4"
      >
        <div 
          v-if="isMenuOpen"
          class="md:hidden absolute left-0 right-0 bg-green-600 z-50 shadow-xl overflow-hidden"
          style="top: 4rem;"
        >
          <div class="container mx-auto px-4 py-2 space-y-1">
            <RouterLink 
              v-for="link in [
                { to: '/', text: 'Accueil' },
                { to: '/about', text: 'À propos' },
                { to: '/contact', text: 'Contact' }
              ]" 
              :key="link.to"
              :to="link.to"
              class="block relative text-white px-3 py-3 rounded-md transition-all duration-300 hover:bg-green-500"
              :class="{ 'bg-green-700': route.path === link.to }"
              @click="toggleMenu"
            >
              <span>{{ link.text }}</span>
              <span 
                class="absolute bottom-2 left-3 right-3 h-0.5 bg-white transition-all duration-300 transform scale-x-0"
                :class="{ 'scale-x-100': route.path === link.to }"
              ></span>
            </RouterLink>
          </div>
        </div>
      </transition>
    </div>
  </nav>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* Animation des liens mobile */
.router-link-active {
  transform: translateX(0);
}
</style>