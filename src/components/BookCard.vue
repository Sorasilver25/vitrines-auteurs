<template>
  <div class="border rounded-xl shadow-md p-4 flex gap-4 mb-6">
    <!-- Carrousel d'images -->
    <div class="relative w-full sm:w-32 h-auto sm:h-48 overflow-hidden relative">
      <div v-for="(img, index) in images" :key="index" 
           :class="['absolute transition-all', { 'opacity-0': index !== currentImageIndex, 'opacity-100': index === currentImageIndex }]">
        <img :src="img" :alt="title" class="w-full h-full object-cover rounded-md" />
      </div>
      <button @click="prevImage" class="absolute top-1/2 left-0 transform -translate-y-1/2 bg-gray-600 text-white p-2 rounded-full sm:block hidden">‹</button>
      <button @click="nextImage" class="absolute top-1/2 right-0 transform -translate-y-1/2 bg-gray-600 text-white p-2 rounded-full sm:block hidden">›</button>
    </div>

    <!-- Info-->
    <div class="ml-4">
      <h3 class="text-xl font-semibold text-gray-800">{{ title }}</h3>
      <span v-if="nouveau" class="bg-green-100 text-green-700 text-xs px-2 py-0.5 rounded-full">Nouveau</span>
        <span v-if="coupDeCoeur" class="bg-pink-100 text-pink-700 text-xs px-2 py-0.5 rounded-full">❤️ Coup de cœur</span>
        <span v-if="promo" class="bg-yellow-100 text-yellow-700 text-xs px-2 py-0.5 rounded-full">Promo</span>
      <p class="text-sm text-gray-600 mt-2">{{ description }}</p>
      
      <!-- Lien vers le site d'achat -->
      <a :href="link" target="_blank" class="text-purple-600 underline block my-2">Découvrir</a>

      <!-- Réseaux sociaux -->
      <div class="flex space-x-3">
        <a v-for="(social, index) in socials" :key="index" :href="social.link" target="_blank" class="text-gray-500 hover:text-purple-600 text-lg">
          <i :class="social.icon" class="text-lg"></i>
        </a>
      </div>

      <!-- Auteur et catégorie -->
      <div class="mt-4 space-y-1 text-sm text-gray-700">
        <p><strong>Auteur:</strong> {{ author }}</p>
        <p><strong>Catégorie:</strong> {{ category }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  title: String,
  description: String,
  link: String,
  images: Array,
  socials: Array,
  author: String,
  category: String,
  nouveau: Boolean,
  coupDeCoeur: Boolean,
  promo: Boolean
})

const currentImageIndex = ref(0)

const resolvedImages = computed(() => {
  return props.images?.map(img => new URL(img, import.meta.url).href) || []
})

const nextImage = () => {
  currentImageIndex.value = (currentImageIndex.value + 1) % resolvedImages.value.length
}

const prevImage = () => {
  currentImageIndex.value =
    (currentImageIndex.value - 1 + resolvedImages.value.length) % resolvedImages.value.length
}
</script>

<style scoped>
i {
  transition: transform 0.2s;
}
i:hover {
  transform: scale(1.15);
}
</style>
