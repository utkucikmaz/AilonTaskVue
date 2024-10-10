<template>
  <div class="p-12">
    <h1 class="text-2xl font-bold mb-6 text-center">WAS KOCHEN WIR HEUTE?</h1>

    <section class="bg-white shadow-md rounded-lg p-6 max-w-xl mx-auto">
      <div class="space-y-6">
        <div class="flex items-center space-x-4 justify-center">
          <label for="effort" class="w-32 text-lg font-medium text-right">Aufwand</label>
          <div class="flex space-x-4">
            <button
              v-for="option in effortOptions"
              :key="option"
              :class="[
                'px-4 py-2 rounded-lg hover:bg-gray-600 hover:text-white',
                effort === option ? 'bg-black text-white' : 'bg-gray-200 text-black'
              ]"
              @click="setEffort(option)"
            >
              {{ option }}
            </button>
          </div>
        </div>

        <div class="flex items-center space-x-4 justify-center">
          <label for="price" class="w-32 text-lg font-medium text-right">Preis</label>
          <div class="flex space-x-4">
            <button
              v-for="option in priceOptions"
              :key="option"
              :class="[
                'px-4 py-2 rounded-lg hover:bg-gray-600 hover:text-white',
                price === option ? 'bg-black text-white' : 'bg-gray-200 text-black'
              ]"
              @click="setPrice(option)"
            >
              {{ option }}
            </button>
          </div>
        </div>

        <div class="flex items-center space-x-4 justify-center">
          <label for="veggie" class="w-32 text-lg font-medium text-right">Vegetarisch</label>
          <div v-for="option in veggieOptions" :key="option" class="flex space-x-4">
            <button
              :class="[
                'px-4 py-2 rounded-lg hover:bg-gray-600 hover:text-white',
                veggie === option ? 'bg-black text-white' : 'bg-gray-200 text-black'
              ]"
              @click="setVeggie(option)"
            >
              {{ option }}
            </button>
          </div>
        </div>
      </div>
    </section>
  </div>

  <div>
    <div class="flex justify-evenly mt-6">
      <button
        class="px-4 py-2 text-white bg-gray-500 rounded-lg hover:bg-blue-600 active:bg-blue-700"
        @click="$emit('handleResetClick')"
      >
        Reset
      </button>
      <button
        class="px-4 py-2 text-white bg-gray-500 rounded-lg hover:bg-blue-600 active:bg-blue-700"
        @click="$emit('handleForwardClick')"
      >
        Weiter
      </button>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps({
  veggieOptions: Array,
  priceOptions: Array,
  effortOptions: Array,
  effort: String,
  price: String,
  veggie: [String, Boolean]
})
const emit = defineEmits([
  'handleResetClick',
  'handleForwardClick',
  'setEffort',
  'setPrice',
  'setVeggie'
])

const setEffort = (value) => {
  emit('setEffort', value)
}

const setPrice = (value) => {
  emit('setPrice', value)
}

const setVeggie = (value) => {
  emit('setVeggie', value)
}
</script>
