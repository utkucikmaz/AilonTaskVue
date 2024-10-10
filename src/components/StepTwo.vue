<template>
  <div class="flex flex-col items-center justify-center p-12">
    <h1 class="text-4xl font-bold mb-8 text-gray-800">WAS KOCHEN WIR HEUTE?</h1>

    <div class="bg-white rounded-lg shadow-lg p-6 w-1/2">
      <div v-if="randomMeal">
        <h2 class="text-2xl font-semibold mb-4 text-gray-700">{{ randomMeal.name }}</h2>
        <div class="flex justify-start">
          <div class="w-1/2 m-2">
            <img
              :src="randomMeal.image"
              alt="picture of the food"
              class="w-full h-48 object-cover rounded-md"
              @error="setNoImage"
            />
          </div>
          <div class="w-1/2 grid justify-center">
            <p class="text-gray-600 mb-2">
              <strong class="font-semibold">Aufwand: {{ randomMeal.effort }}</strong>
            </p>
            <p class="text-gray-600 mb-2">
              <strong class="font-semibold">Kosten: {{ randomMeal.cost }}</strong>
            </p>
            <p class="text-gray-600 mb-4">
              <strong class="font-semibold">Vegetarisch: {{ randomMeal.veggie }}</strong>
            </p>

            <h3 class="text-xl font-medium mb-2 text-gray-700">Einkaufsliste</h3>
            <ul class="list-decimal list-inside text-gray-600">
              <li v-for="item in randomMeal.ingredients" :key="item">{{ item }}</li>
            </ul>
          </div>
        </div>
      </div>
      <div v-else class="flex items-center justify-center">
        <p class="my-8">Es gibt keine Mahlzeit unter dieser Auswahl</p>
      </div>
    </div>
  </div>

  <div class="flex justify-evenly mt-6 mx-8">
    <button
      class="px-4 py-2 text-white bg-gray-500 rounded-md hover:bg-blue-600 active:bg-blue-700"
      @click="$emit('handleBackClick')"
    >
      Zurück
    </button>
    <button
      class="px-4 py-2 text-white bg-gray-500 rounded-md hover:bg-blue-600 active:bg-blue-700"
      @click="$emit('handleRandomizeClick')"
    >
      Randomize
    </button>
  </div>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue'
import noImage from '@/assets/no-image.jpg'

const setNoImage = (event) => {
  event.target.src = noImage
}

defineProps({
  randomMeal: Object
})
defineEmits(['handleBackClick', 'handleRandomizeClick'])
</script>
