<template>
  <footer class="bg-gray-900 text-white">
    <!-- Section principale du footer -->
    <div class="max-w-7xl mx-auto px-3 sm:px-6 lg:px-8 py-8 sm:py-12">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 sm:gap-8">
        <!-- À propos -->
        <div class="md:col-span-2">
          <div class="flex items-center space-x-2 sm:space-x-3 mb-3 sm:mb-4">
            <div class="w-8 h-8 sm:w-10 sm:h-10 bg-gradient-to-r from-indigo-600 to-purple-600 rounded-lg flex items-center justify-center">
              <i class="fas fa-book-open text-white text-sm sm:text-lg"></i>
            </div>
            <h3 class="font-display text-lg sm:text-xl font-bold">Vitrine Auteurs</h3>
          </div>
          <p class="text-gray-300 leading-relaxed mb-4 sm:mb-6 max-w-md text-sm sm:text-base">
            Notre mission est de mettre en lumière les talents de l'auto-édition et de créer un pont entre les auteurs indépendants et leurs futurs lecteurs.
          </p>
          <div class="flex space-x-3 sm:space-x-4">
            <a href="https://instagram.com/evil._night._" target="_blank" 
               class="w-9 h-9 sm:w-10 sm:h-10 bg-gray-800 hover:bg-indigo-600 rounded-lg flex items-center justify-center transition-all duration-300 touch-manipulation">
              <i class="fab fa-instagram text-sm sm:text-base"></i>
            </a>
          </div>
        </div>

        <!-- Informations légales -->
        <div>
          <h4 class="font-semibold text-base sm:text-lg mb-3 sm:mb-4">Informations légales</h4>
          <ul class="space-y-2 sm:space-y-3">
            <li>
              <button @click="showPrivacyModal = true" class="text-gray-300 hover:text-white transition-colors duration-200 text-left text-sm sm:text-base p-1 -m-1 touch-manipulation">
                Politique de confidentialité
              </button>
            </li>
            <li>
              <button @click="showTermsModal = true" class="text-gray-300 hover:text-white transition-colors duration-200 text-left text-sm sm:text-base p-1 -m-1 touch-manipulation">
                Conditions d'utilisation
              </button>
            </li>
            <li>
              <button @click="showLegalModal = true" class="text-gray-300 hover:text-white transition-colors duration-200 text-left text-sm sm:text-base p-1 -m-1 touch-manipulation">
                Mentions légales
              </button>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Section copyright -->
    <div class="border-t border-gray-800">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
        <div class="flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0">
          <div class="text-gray-400 text-sm">
            © {{ currentYear }} Vitrine Auteurs. Tous droits réservés aux auteurs pour leurs œuvres.
          </div>
          <div class="text-gray-400 text-sm">
            Projet open source communautaire
          </div>
        </div>
        
        <!-- Message sur la confidentialité -->
        <div class="mt-4 pt-4 border-t border-gray-800">
          <div class="flex items-center justify-center space-x-2 text-gray-400 text-sm">
            <i class="fas fa-shield-alt text-green-400"></i>
            <span>Aucune collecte de données personnelles - Votre vie privée est respectée</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Bouton retour en haut -->
    <button @click="scrollToTop" 
            class="fixed bottom-6 right-6 w-12 h-12 bg-indigo-600 hover:bg-indigo-700 text-white rounded-full shadow-lg flex items-center justify-center transition-all duration-300 transform hover:scale-110 z-40">
      <i class="fas fa-arrow-up"></i>
    </button>

    <!-- Modales des pages légales -->
    <PrivacyPolicy v-if="showPrivacyModal" @close="showPrivacyModal = false" />
    <TermsOfService v-if="showTermsModal" @close="showTermsModal = false" />
    <LegalNotices v-if="showLegalModal" @close="showLegalModal = false" />
  </footer>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import PrivacyPolicy from './legal/PrivacyPolicy.vue'
import TermsOfService from './legal/TermsOfService.vue'
import LegalNotices from './legal/LegalNotices.vue'

const currentYear = ref(new Date().getFullYear())
const showPrivacyModal = ref(false)
const showTermsModal = ref(false)
const showLegalModal = ref(false)

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}

onMounted(() => {
  // Animation d'apparition du bouton selon le scroll
  window.addEventListener('scroll', () => {
    const button = document.querySelector('.fixed.bottom-6')
    if (button) {
      if (window.scrollY > 300) {
        button.style.opacity = '1'
        button.style.transform = 'scale(1)'
      } else {
        button.style.opacity = '0'
        button.style.transform = 'scale(0.8)'
      }
    }
  })
})
</script>

<style scoped>
.fixed.bottom-6 {
  transition: opacity 0.3s ease, transform 0.3s ease;
}
</style>
