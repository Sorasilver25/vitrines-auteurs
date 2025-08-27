<template>
  <article class="card p-3 md:p-4 bg-card-gradient group cursor-pointer" @click="$emit('openDetail')">
    <div class="flex flex-col gap-3 md:gap-4">
      <!-- Section image responsive et compacte -->
      <div class="flex-shrink-0">
        <div class="relative w-full h-40 sm:h-44 md:h-48 overflow-hidden rounded-xl bg-gray-100">
          <!-- Image par défaut si aucune image -->
          <div v-if="!images || images.length === 0" 
               class="w-full h-full flex items-center justify-center bg-gradient-to-br from-gray-200 to-gray-300">
            <div class="text-center">
              <i class="fas fa-book text-2xl md:text-3xl text-gray-400 mb-2"></i>
              <p class="text-xs text-gray-500 font-medium">Couverture</p>
              <p class="text-xs text-gray-400">à venir</p>
            </div>
          </div>
          
          <!-- Carrousel d'images -->
          <div v-else class="relative w-full h-full">
            <div v-for="(img, index) in processedImages" :key="index" 
                 :class="['absolute inset-0 transition-all duration-500', 
                         { 'opacity-0 scale-105': index !== currentImageIndex, 
                           'opacity-100 scale-100': index === currentImageIndex }]">
              <img :src="img" :alt="title" 
                   class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-105" 
                   loading="lazy" />
            </div>
            
            <!-- Contrôles du carrousel - visibles sur mobile, au survol sur desktop -->
            <div v-if="processedImages.length > 1" class="absolute inset-0 flex items-center justify-between p-2 opacity-100 md:opacity-0 group-hover:opacity-100 transition-opacity duration-300">
              <button @click="prevImage" 
                      class="w-7 h-7 md:w-8 md:h-8 bg-black bg-opacity-50 text-white rounded-full flex items-center justify-center hover:bg-opacity-75 transition-all touch-target">
                <i class="fas fa-chevron-left text-xs"></i>
              </button>
              <button @click="nextImage" 
                      class="w-7 h-7 md:w-8 md:h-8 bg-black bg-opacity-50 text-white rounded-full flex items-center justify-center hover:bg-opacity-75 transition-all touch-target">
                <i class="fas fa-chevron-right text-xs"></i>
              </button>
            </div>
            
            <!-- Indicateurs -->
            <div v-if="processedImages.length > 1" class="absolute bottom-2 left-1/2 transform -translate-x-1/2 flex space-x-1">
              <button v-for="(_, index) in processedImages" :key="index"
                      @click="currentImageIndex = index"
                      :class="['w-1.5 h-1.5 md:w-2 md:h-2 rounded-full transition-all touch-target', 
                              index === currentImageIndex ? 'bg-white' : 'bg-white bg-opacity-50']">
              </button>
            </div>
          </div>
        </div>
      </div>

      <!-- Section contenu responsive et compacte -->
      <div class="flex-1 space-y-2 md:space-y-3">
        <!-- En-tête avec badges -->
        <div class="space-y-2">
          <div class="flex flex-wrap gap-1">
            <span v-if="nouveau" class="badge badge-new text-xs">
              <i class="fas fa-star mr-1"></i>
              Nouveau
            </span>
            <span v-if="coupDeCoeur" class="badge badge-heart text-xs">
              <i class="fas fa-heart mr-1"></i>
              <span class="hidden sm:inline">Coup de cœur</span>
              <span class="sm:hidden">❤️</span>
            </span>
            <span v-if="promo" class="badge badge-promo text-xs">
              <i class="fas fa-tag mr-1"></i>
              Promo
            </span>
            <span v-if="wattpad" class="badge badge-wattpad text-xs">
              <i class="fab fa-wattpad mr-1"></i>
              Wattpad
            </span>
          </div>
          
          <h3 class="font-display text-base md:text-lg lg:text-xl font-bold text-gray-900 leading-tight group-hover:text-indigo-600 transition-colors duration-300">
            {{ title }}
          </h3>
        </div>

        <!-- Métadonnées compactes -->
        <div class="space-y-1 text-xs md:text-sm">
          <div class="flex items-center text-gray-700">
            <i class="fas fa-user mr-1.5 text-gray-400 text-xs"></i>
            <span class="font-medium truncate">{{ author }}</span>
          </div>
          <div class="flex items-center text-gray-700">
            <i class="fas fa-bookmark mr-1.5 text-gray-400 text-xs"></i>
            <span class="truncate">{{ category }}</span>
          </div>
        </div>

        <!-- Description compacte -->
        <p class="text-gray-600 leading-relaxed text-xs md:text-sm line-clamp-2">{{ description }}</p>

        <!-- Actions compactes -->
        <div class="flex flex-col gap-2 pt-2">
          <a :href="link" target="_blank" 
             class="btn-primary w-full text-center inline-flex items-center justify-center text-xs md:text-sm touch-target py-2"
             @click.stop>
            <i class="fas fa-external-link-alt mr-1.5"></i>
            Découvrir
          </a>
          
          <!-- Réseaux sociaux compacts -->
          <div v-if="socials && socials.length > 0" class="flex items-center justify-center gap-2">
            <span class="text-xs text-gray-500 hidden sm:block">Suivre :</span>
            <div class="flex gap-1.5">
              <a v-for="(social, index) in socials" :key="index" 
                 :href="social.link" target="_blank" 
                 class="w-8 h-8 bg-gray-100 hover:bg-indigo-600 text-gray-600 hover:text-white rounded-lg flex items-center justify-center transition-all duration-300 transform hover:scale-110 touch-target"
                 @click.stop>
                <i :class="social.icon" class="text-sm"></i>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>

<script setup>
import { ref, computed } from 'vue'

const emit = defineEmits(['openDetail'])

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

// Traitement des images avec gestion d'erreur
const processedImages = computed(() => {
  if (!props.images || props.images.length === 0) return []
  
  return props.images.map(img => {
    if (img.startsWith('http')) return img
    return img.startsWith('/') ? img : `/${img}`
  })
})

const nextImage = () => {
  if (processedImages.value.length > 0) {
    currentImageIndex.value = (currentImageIndex.value + 1) % processedImages.value.length
  }
}

const prevImage = () => {
  if (processedImages.value.length > 0) {
    currentImageIndex.value = (currentImageIndex.value - 1 + processedImages.value.length) % processedImages.value.length
  }
}

// Auto-rotation des images toutes les 5 secondes
let autoRotateInterval
const startAutoRotate = () => {
  if (processedImages.value.length > 1) {
    autoRotateInterval = setInterval(nextImage, 5000)
  }
}

const stopAutoRotate = () => {
  if (autoRotateInterval) {
    clearInterval(autoRotateInterval)
  }
}

// Gestion des événements de survol
const onMouseEnter = () => stopAutoRotate()
const onMouseLeave = () => startAutoRotate()

// Démarrer l'auto-rotation au montage
import { onMounted, onUnmounted } from 'vue'

onMounted(() => {
  startAutoRotate()
})

onUnmounted(() => {
  stopAutoRotate()
})
</script>

<style scoped>
/* Animations personnalisées pour les images */
@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.slide-in {
  animation: slideIn 0.5s ease-out;
}

/* Effet de survol sur les liens sociaux */
.social-link {
  position: relative;
  overflow: hidden;
}

.social-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
  transition: left 0.5s;
}

.social-link:hover::before {
  left: 100%;
}
</style>
