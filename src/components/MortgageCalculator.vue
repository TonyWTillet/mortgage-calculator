<template>
  <div class="container py-8">
    <div class="max-w-2xl mx-auto bg-white rounded-lg shadow-md p-6">
      <h1 class="text-3xl font-bold text-gray-900 mb-6">Calculateur de mensualités</h1>
      
      <div class="space-y-6">
        <!-- Informations du prêt -->
        <div class="bg-gray-50 p-4 rounded-lg">
          <h2 class="text-xl font-bold text-gray-900 mb-4">Informations du prêt</h2>
          <div class="space-y-4">

            <!-- Prix d'achat -->
            <div>
              <label for="purchasePrice" class="block text-sm font-medium text-gray-700 mb-1">
                Prix d'achat (€)
              </label>
              <input
                v-model="purchasePrice"
                type="number"
                name="purchasePrice"
                id="purchasePrice" 
                class="input-field"
                placeholder="Ex: 250000"
                min="0"
              />
            </div>

            <!-- Apport initial -->
            <div>
              <label for="initialDeposit" class="block text-sm font-medium text-gray-700 mb-1">
                Apport initial (€)
              </label>
              <input
                v-model="initialDeposit"
                type="number"
                name="initialDeposit"
                id="initialDeposit"
                class="input-field"
                placeholder="Ex: 50000"
                min="0"
              />
            </div>

            <!-- Montant du prêt -->
            <div>
              <label for="loanAmount" class="block text-sm font-medium text-gray-700 mb-1">
                Montant du prêt (€)
              </label>
              <input
                v-model="loanAmount"
                type="number"
                name="loanAmount"
                id="loanAmount"
                class="input-field"
                placeholder="Ex: 200000"
                min="0"
              />
            </div>

            <!-- Durée du prêt -->
            <div>
              <label for="loanTerm" class="block text-sm font-medium text-gray-700 mb-1">
                Durée du prêt (années)
              </label>
              <input
                v-model="loanTerm"
                type="number"
                name="loanTerm"
                id="loanTerm"
                class="input-field"
                placeholder="Ex: 25"
                min="1"
                max="30"
              />
            </div>

            <!-- Taux d'intérêt -->
            <div>
              <label for="interestRate" class="block text-sm font-medium text-gray-700 mb-1">
                Taux d'intérêt annuel (%)
              </label>
              <input
                v-model="interestRate"
                type="number"
                name="interestRate"
                id="interestRate"
                class="input-field"
                placeholder="Ex: 3.5"
                step="0.1"
                min="0"
                max="15"
              />
            </div>

          </div>
          
          <!-- Résultats de simulation -->
          <div v-if="monthlyPayment > 0">
            <div class="my-5 bg-white p-6 rounded-lg shadow-md border border-amber-100 mb-4">
              <h3 class="text-xl font-semibold text-slate-700 mb-4">Résultats de simulation</h3>
              
              <div class="space-y-4">
                <div class="flex justify-between items-center border-b border-amber-100 pb-2">
                  <span class="text-slate-600">Mensualité totale</span>
                  <span class="text-xl font-bold text-amber-600">{{ monthlyPayment.toFixed(2) }} €/mois</span>
                </div>

                <div class="flex justify-between items-center">
                  <span class="text-slate-600">Coût total du crédit</span>
                  <span class="text-lg font-semibold text-amber-600">{{ (monthlyPayment * loanTerm * 12).toFixed(2) }} €</span>
                </div>
              </div>
            </div>
            <span class="text-sm text-gray-500">
              *Les taux d'intérêt sont estimés et peuvent varier en fonction de votre situation financière.
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const purchasePrice = ref(0);
const initialDeposit = ref(0);
const loanTerm = ref(0);
const interestRate = ref(0);

// Calcul du montant du prêt
const loanAmount = computed(() => {
  return purchasePrice.value - initialDeposit.value;
});

// Calcul de la mensualité
const monthlyPayment = computed(() => {
  const rate = interestRate.value / 100 / 12;
  const n = loanTerm.value * 12;
  return (loanAmount.value * rate * Math.pow(1 + rate, n)) / (Math.pow(1 + rate, n) - 1);
});
</script>

<style scoped>
/* Additional component-specific styles can go here */
</style> 