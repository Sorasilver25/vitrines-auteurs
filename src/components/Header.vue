<template>
  <header class="bg-purple-600 text-white p-4 flex justify-between items-center">
    <h1 class="text-xl font-bold">Vitrine Auteurs</h1>
    <nav class="space-x-4">
      <button @click="showModal = true" class="hover:underline">Nous rejoindre</button>
    </nav>

    <!-- Modal -->
    <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
      <div class="bg-white text-black p-6 rounded-xl shadow-lg w-80 relative">
        <h2 class="text-xl font-semibold mb-2">Nous rejoindre</h2>
        <!-- <p class="mb-2">Tu peux me contacter par mail à :</p>
        <p class="text-purple-700 font-medium mb-2">adresse@email.com</p> -->
        <p class="mb-2">Tu peux me contacter via Instagram ici</p>
        <a href="https://instagram.com/evil._night._" target="_blank" class="text-blue-600 underline">evil._night._</a>

        <button @click="showModal = false" class="absolute top-2 right-3 text-gray-500 hover:text-gray-700 text-xl">&times;</button>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'

const showModal = ref(false)
</script>
