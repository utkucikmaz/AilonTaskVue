<script setup>
import { ref, computed } from 'vue'
import allMeals from '@/db/meals.json'
import StepOne from '@/components/StepOne.vue'
import StepTwo from '@/components/StepTwo.vue'

const step = ref(1)
const effort = ref('egal')
const price = ref('egal')
const veggie = ref('egal')
const randomMeal = ref(null)

const effortOptions = ['egal', 'low', 'high']
const priceOptions = ['egal', 'low', 'high']
const veggieOptions = ['egal', true, false]

const setEffort = (value) => (effort.value = value)
const setPrice = (value) => (price.value = value)
const setVeggie = (value) => (veggie.value = value)

const meals = computed(() => {
  return allMeals.filter(
    (meal) =>
      (effort.value === 'egal' || effort.value === meal.effort) &&
      (price.value === 'egal' || price.value === meal.cost) &&
      (veggie.value === 'egal' || veggie.value === meal.veggie)
  )
})
const setRandomIndex = () => {
  randomMeal.value = meals.value[Math.floor(Math.random() * meals.value.length)]
}

const handleForwardClick = () => {
  setRandomIndex()
  step.value = 2
}
const handleBackClick = () => (step.value = 1)
const handleResetClick = () => {
  effort.value = 'egal'
  price.value = 'egal'
  veggie.value = 'egal'
}
const handleRandomizeClick = () => {
  setRandomIndex()
}
</script>

<template>
  <div class="container mx-auto">
    <div v-if="step === 1" class="container mx-auto pt-10 items-center justify-center">
      <StepOne
        :effort-options="effortOptions"
        :price-options="priceOptions"
        :veggie-options="veggieOptions"
        :effort="effort"
        :price="price"
        :veggie="veggie"
        @handleResetClick="handleResetClick"
        @handleForwardClick="handleForwardClick"
        @setEffort="setEffort"
        @setPrice="setPrice"
        @setVeggie="setVeggie"
      />
    </div>

    <div v-else class="container mx-auto mt-16 max-w-7xl items-center justify-center">
      <StepTwo
        :random-meal="randomMeal"
        @handleBackClick="handleBackClick"
        @handleRandomizeClick="handleRandomizeClick"
      />
    </div>
  </div>
</template>
