<template>
  <div class="flex flex-col sm:flex-row bg-white rounded-2xl shadow-lg overflow-hidden mb-6 border border-gray-200">
    <!-- Carrousel d'images -->
    <div class="relative w-full sm:w-40 h-60 flex-shrink-0">
      <img
        :src="resolvedImages[currentImageIndex]"
        :alt="title"
        class="w-full h-full object-cover"
      />
      <button
        @click="prevImage"
        class="absolute top-1/2 left-2 -translate-y-1/2 bg-white/70 hover:bg-white p-1 rounded-full shadow text-gray-600"
      >
        ‹
      </button>
      <button
        @click="nextImage"
        class="absolute top-1/2 right-2 -translate-y-1/2 bg-white/70 hover:bg-white p-1 rounded-full shadow text-gray-600"
      >
        ›
      </button>
    </div>

    <!-- Infos -->
    <div class="flex-1 p-4 flex flex-col justify-between">
      <div>
        <h3 class="text-xl font-semibold text-gray-800">{{ title }}</h3>
        <span v-if="nouveau" class="bg-green-100 text-green-700 text-xs px-2 py-0.5 rounded-full">Nouveau</span>
        <span v-if="coupDeCoeur" class="bg-pink-100 text-pink-700 text-xs px-2 py-0.5 rounded-full">❤️ Coup de cœur</span>
        <span v-if="promo" class="bg-yellow-100 text-yellow-700 text-xs px-2 py-0.5 rounded-full">Promo</span>
        <p class="text-sm text-gray-600 mt-2">{{ description }}</p>
      </div>

      <div class="mt-4 space-y-1 text-sm text-gray-700">
        <p><strong>Auteur :</strong> {{ author }}</p>
        <p><strong>Catégorie :</strong> {{ category }}</p>
      </div>

      <!-- Lien + Réseaux -->
      <div class="mt-4 flex items-center justify-between">
        <a
          :href="link"
          target="_blank"
          class="text-sm text-purple-600 hover:underline font-medium bg-purple-100 px-3 py-1 rounded-full"
        >
          Découvrir
        </a>
        <div class="flex space-x-3">
          <a
            v-for="(social, index) in socials"
            :key="index"
            :href="social.link"
            target="_blank"
            class="text-gray-500 hover:text-purple-600 text-lg"
          >
            <i :class="social.icon"></i>
          </a>
        </div>
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
