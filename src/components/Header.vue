<template>
  <!-- Navigation sticky -->
  <nav class="bg-white shadow-lg sticky top-0 z-50 border-b border-gray-100">
    <div class="max-w-7xl mx-auto px-3 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-14 sm:h-16">
        <!-- Logo et titre -->
        <div class="flex items-center space-x-2 sm:space-x-3">
          <div class="flex-shrink-0">
            <div class="w-8 h-8 sm:w-10 sm:h-10 bg-gradient-to-r from-indigo-600 to-purple-600 rounded-lg flex items-center justify-center">
              <i class="fas fa-book-open text-white text-sm sm:text-lg"></i>
            </div>
          </div>
          <div>
            <h1 class="font-display text-lg sm:text-xl font-bold text-gray-900">Vitrine Auteurs</h1>
          </div>
        </div>

        <!-- Bouton nous rejoindre -->
        <div class="flex items-center">
          <button @click="showModal = true" class="btn-primary text-sm sm:text-base px-3 py-1.5 sm:px-4 sm:py-2">
            <i class="fas fa-users mr-1 sm:mr-2"></i>
            <span class="hidden xs:inline">Nous </span>rejoindre
          </button>
        </div>
      </div>
    </div>
  </nav>

  <!-- Modal améliorée -->
  <Transition name="modal">
    <div v-if="showModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-3 sm:p-4">
      <div class="bg-white rounded-2xl shadow-2xl w-full max-w-sm sm:max-w-md relative transform transition-all mx-2">
        <div class="p-6 sm:p-8">
          <div class="text-center mb-4 sm:mb-6">
            <div class="w-12 h-12 sm:w-16 sm:h-16 bg-gradient-to-r from-indigo-600 to-purple-600 rounded-full flex items-center justify-center mx-auto mb-3 sm:mb-4">
              <i class="fas fa-handshake text-white text-lg sm:text-2xl"></i>
            </div>
            <h2 class="font-display text-xl sm:text-2xl font-bold text-gray-900 mb-2">Rejoignez notre communauté</h2>
            <p class="text-sm sm:text-base text-gray-600">Partagez votre passion pour l'écriture avec nous</p>
          </div>
          
          <div class="space-y-3 sm:space-y-4">
            <div class="bg-gray-50 rounded-lg p-3 sm:p-4">
              <h3 class="font-semibold text-gray-900 mb-2 text-sm sm:text-base">Contactez-nous sur Instagram</h3>
              <a href="https://instagram.com/evil._night._" target="_blank" 
                 class="flex items-center justify-center space-x-2 text-pink-600 hover:text-pink-700 transition-colors p-2 -m-2 rounded-lg touch-manipulation">
                <i class="fab fa-instagram text-lg sm:text-xl"></i>
                <span class="font-medium text-sm sm:text-base">@evil._night._</span>
                <i class="fas fa-external-link-alt text-xs sm:text-sm"></i>
              </a>
            </div>
            
            <div class="text-center text-xs sm:text-sm text-gray-500">
              <p>Nous avons hâte de découvrir votre univers littéraire !</p>
            </div>
          </div>
        </div>
        
        <button @click="showModal = false" 
                class="absolute top-3 right-3 sm:top-4 sm:right-4 w-8 h-8 sm:w-10 sm:h-10 bg-gray-100 hover:bg-gray-200 rounded-full flex items-center justify-center transition-colors touch-manipulation">
          <i class="fas fa-times text-gray-600 text-sm sm:text-base"></i>
        </button>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { ref } from 'vue'

const showModal = ref(false)
</script>

<style scoped>
.modal-enter-active, .modal-leave-active {
  transition: all 0.3s ease;
}

.modal-enter-from, .modal-leave-to {
  opacity: 0;
  transform: scale(0.9);
}
</style>
