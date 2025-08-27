<template>
  <!-- Modal backdrop -->
  <Transition name="modal">
    <div v-if="show" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-3 sm:p-4" @click="$emit('close')">
      <div class="bg-white rounded-2xl shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-hidden relative transform transition-all mx-2" @click.stop>
        <!-- Header avec bouton fermer -->
        <div class="sticky top-0 bg-white border-b border-gray-200 px-4 sm:px-6 py-4 flex items-center justify-between z-10">
          <div class="flex items-center space-x-3">
            <div class="w-8 h-8 bg-gradient-to-r from-indigo-600 to-purple-600 rounded-lg flex items-center justify-center">
              <i class="fas fa-book-open text-white text-sm"></i>
            </div>
            <h2 class="font-display text-lg sm:text-xl font-bold text-gray-900 truncate">Détails de l'œuvre</h2>
          </div>
          <button @click="$emit('close')" 
                  class="w-8 h-8 sm:w-10 sm:h-10 bg-gray-100 hover:bg-gray-200 rounded-full flex items-center justify-center transition-colors touch-manipulation">
            <i class="fas fa-times text-gray-600 text-sm sm:text-base"></i>
          </button>
        </div>

        <!-- Contenu scrollable -->
        <div class="overflow-y-auto max-h-[calc(90vh-80px)]">
          <div class="p-4 sm:p-6">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 lg:gap-8">
              <!-- Section image -->
              <div class="space-y-4">
                <!-- Image principale -->
                <div class="relative w-full aspect-[3/4] max-w-sm mx-auto lg:max-w-none overflow-hidden rounded-xl bg-gray-100">
                  <div v-if="!book.images || book.images.length === 0" 
                       class="w-full h-full flex items-center justify-center bg-gradient-to-br from-gray-200 to-gray-300">
                    <div class="text-center">
                      <i class="fas fa-book text-4xl md:text-5xl text-gray-400 mb-3"></i>
                      <p class="text-sm md:text-base text-gray-500 font-medium">Couverture</p>
                      <p class="text-xs text-gray-400">à venir</p>
                    </div>
                  </div>
                  
                  <div v-else class="relative w-full h-full">
                    <div v-for="(img, index) in processedImages" :key="index" 
                         :class="['absolute inset-0 transition-all duration-500', 
                                 { 'opacity-0 scale-105': index !== currentImageIndex, 
                                   'opacity-100 scale-100': index === currentImageIndex }]">
                      <img :src="img" :alt="book.title" 
                           class="w-full h-full object-cover" 
                           loading="lazy" />
                    </div>
                    
                    <!-- Contrôles carrousel -->
                    <div v-if="processedImages.length > 1" class="absolute inset-0 flex items-center justify-between p-3 opacity-0 hover:opacity-100 transition-opacity duration-300">
                      <button @click="prevImage" 
                              class="w-10 h-10 bg-black bg-opacity-50 text-white rounded-full flex items-center justify-center hover:bg-opacity-75 transition-all touch-target">
                        <i class="fas fa-chevron-left"></i>
                      </button>
                      <button @click="nextImage" 
                              class="w-10 h-10 bg-black bg-opacity-50 text-white rounded-full flex items-center justify-center hover:bg-opacity-75 transition-all touch-target">
                        <i class="fas fa-chevron-right"></i>
                      </button>
                    </div>
                    
                    <!-- Indicateurs -->
                    <div v-if="processedImages.length > 1" class="absolute bottom-3 left-1/2 transform -translate-x-1/2 flex space-x-2">
                      <button v-for="(_, index) in processedImages" :key="index"
                              @click="currentImageIndex = index"
                              :class="['w-2 h-2 rounded-full transition-all touch-target', 
                                      index === currentImageIndex ? 'bg-white' : 'bg-white bg-opacity-50']">
                      </button>
                    </div>
                  </div>
                </div>

                <!-- Actions principales -->
                <div class="space-y-3">
                  <a :href="book.link" target="_blank" 
                     class="btn-primary w-full text-center inline-flex items-center justify-center text-sm touch-target">
                    <i class="fas fa-external-link-alt mr-2"></i>
                    Lire le livre complet
                  </a>
                  
                  <!-- Réseaux sociaux -->
                  <div v-if="book.socials && book.socials.length > 0" class="flex items-center justify-center gap-3">
                    <span class="text-sm text-gray-500">Suivre l'auteur :</span>
                    <div class="flex gap-2">
                      <a v-for="(social, index) in book.socials" :key="index" 
                         :href="social.link" target="_blank" 
                         class="w-10 h-10 bg-gray-100 hover:bg-indigo-600 text-gray-600 hover:text-white rounded-lg flex items-center justify-center transition-all duration-300 transform hover:scale-110 touch-target">
                        <i :class="social.icon" class="text-lg"></i>
                      </a>
                    </div>
                  </div>
                </div>
              </div>

              <!-- Section informations -->
              <div class="space-y-6">
                <!-- Titre et badges -->
                <div class="space-y-3">
                  <div class="flex flex-wrap gap-2">
                    <span v-if="book.nouveau" class="badge badge-new">
                      <i class="fas fa-star mr-1"></i>
                      Nouveau
                    </span>
                    <span v-if="book.coupDeCoeur" class="badge badge-heart">
                      <i class="fas fa-heart mr-1"></i>
                      Coup de cœur
                    </span>
                    <span v-if="book.promo" class="badge badge-promo">
                      <i class="fas fa-tag mr-1"></i>
                      Promo
                    </span>
                    <span v-if="book.wattpad" class="badge badge-wattpad">
                      <i class="fab fa-wattpad mr-1"></i>
                      Wattpad
                    </span>
                  </div>
                  
                  <h1 class="font-display text-2xl sm:text-3xl font-bold text-gray-900 leading-tight">
                    {{ book.title }}
                  </h1>
                </div>

                <!-- Métadonnées principales -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div class="space-y-3">
                    <div class="flex items-center text-gray-700">
                      <i class="fas fa-user mr-3 text-gray-400 w-5"></i>
                      <div>
                        <span class="text-sm text-gray-500">Auteur</span>
                        <p class="font-medium">{{ book.author }}</p>
                      </div>
                    </div>
                    
                    <div class="flex items-center text-gray-700">
                      <i class="fas fa-bookmark mr-3 text-gray-400 w-5"></i>
                      <div>
                        <span class="text-sm text-gray-500">Genre</span>
                        <p class="font-medium">{{ book.category }}</p>
                      </div>
                    </div>
                  </div>

                  <!-- Informations supplémentaires (POC) -->
                  <div class="space-y-3">
                    <div class="flex items-center text-gray-700">
                      <i class="fas fa-calendar mr-3 text-gray-400 w-5"></i>
                      <div>
                        <span class="text-sm text-gray-500">Date de sortie</span>
                        <p class="font-medium">{{ book.releaseDate || 'À déterminer' }}</p>
                      </div>
                    </div>
                    
                    <div class="flex items-center text-gray-700">
                      <i class="fas fa-check-circle mr-3 text-gray-400 w-5"></i>
                      <div>
                        <span class="text-sm text-gray-500">Statut</span>
                        <p class="font-medium">
                          <span v-if="book.completed" class="text-green-600">
                            <i class="fas fa-check mr-1"></i>Terminé
                          </span>
                          <span v-else class="text-orange-600">
                            <i class="fas fa-clock mr-1"></i>En cours
                          </span>
                        </p>
                      </div>
                    </div>
                  </div>
                </div>

                <!-- Description complète -->
                <div class="space-y-3">
                  <h3 class="font-semibold text-gray-900 text-lg">Résumé</h3>                  
                  <!-- Description étendue (POC) -->
                  <div v-if="book.extendedDescription" class="mt-4">
                    <p class="text-gray-600 leading-relaxed">{{ book.extendedDescription }}</p>
                  </div>
                </div>

                <!-- Informations techniques (POC) -->
                <div v-if="book.pageCount || book.isbn || book.language" class="space-y-3">
                  <h3 class="font-semibold text-gray-900 text-lg">Informations techniques</h3>
                  <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-sm">
                    <div v-if="book.pageCount" class="flex items-center">
                      <i class="fas fa-file-alt mr-2 text-gray-400"></i>
                      <span>{{ book.pageCount }} pages</span>
                    </div>
                    <div v-if="book.language" class="flex items-center">
                      <i class="fas fa-globe mr-2 text-gray-400"></i>
                      <span>{{ book.language }}</span>
                    </div>
                    <div v-if="book.isbn" class="flex items-center">
                      <i class="fas fa-barcode mr-2 text-gray-400"></i>
                      <span>ISBN : {{ book.isbn }}</span>
                    </div>
                    <div v-if="book.rating" class="flex items-center">
                      <i class="fas fa-star mr-2 text-yellow-400"></i>
                      <span>{{ book.rating }}/5</span>
                    </div>
                  </div>
                </div>

                <!-- Mots-clés/Tags (POC) -->
                <div v-if="book.tags && book.tags.length > 0" class="space-y-3">
                  <h3 class="font-semibold text-gray-900 text-lg">Mots-clés</h3>
                  <div class="flex flex-wrap gap-2">
                    <span v-for="tag in book.tags" :key="tag" 
                          class="px-3 py-1 bg-gray-100 text-gray-700 rounded-full text-sm hover:bg-gray-200 transition-colors">
                      #{{ tag }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const emit = defineEmits(['close'])

const props = defineProps({
  show: {
    type: Boolean,
    default: false
  },
  book: {
    type: Object,
    default: () => ({})
  }
})

const currentImageIndex = ref(0)

const processedImages = computed(() => {
  if (!props.book.images || props.book.images.length === 0) return []
  
  return props.book.images.map(img => {
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

// Reset image index when book changes
watch(() => props.book, () => {
  currentImageIndex.value = 0
})

// Close modal on escape key
watch(() => props.show, (newValue) => {
  if (newValue) {
    const handleEscape = (e) => {
      if (e.key === 'Escape') {
        emit('close')
      }
    }
    document.addEventListener('keydown', handleEscape)
    // Prevent body scroll when modal is open
    document.body.style.overflow = 'hidden'
    
    return () => {
      document.removeEventListener('keydown', handleEscape)
      document.body.style.overflow = ''
    }
  } else {
    document.body.style.overflow = ''
  }
})
</script>

<style scoped>
.modal-enter-active, .modal-leave-active {
  transition: all 0.3s ease;
}

.modal-enter-from, .modal-leave-to {
  opacity: 0;
  transform: scale(0.9);
}

.touch-target {
  min-height: 44px;
  min-width: 44px;
}
</style>
