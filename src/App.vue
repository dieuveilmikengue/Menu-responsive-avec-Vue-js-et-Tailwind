<script setup lang="ts">
import { RouterView } from 'vue-router'
import NavBarGlass from './components/NavBarGlass.vue';
// import NavBar from './components/NavBar.vue';
</script>

<template>
  <!-- <NavBar /> -->
   <NavBarGlass />
  <main class="container mx-auto p-4">
    <RouterView />
  </main>
</template>