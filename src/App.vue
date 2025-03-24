<script setup>
import MortgageCalculator from './components/MortgageCalculator.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <Header />
    <main class="flex-grow flex items-center justify-center py-8">
      <MortgageCalculator />
    </main>
    <Footer />
  </div>
</template>

<style>
@import './assets/main.css';
</style>
