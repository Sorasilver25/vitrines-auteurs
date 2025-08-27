<template>
  <div class="min-h-screen bg-gray-50">
    <Header />
    
    <!-- Section des filtres statique -->
    <section class="bg-white shadow-sm border-b border-gray-200 sticky top-16 z-40">
      <div class="max-w-7xl mx-auto px-3 sm:px-6 lg:px-8 py-3 md:py-4">
        <div class="flex flex-col gap-3 md:gap-4">
          <!-- Filtres responsive -->
          <div class="flex flex-wrap gap-2 justify-center md:justify-start">
            <button 
              @click="activeFilter = 'all'"
              :class="['px-3 py-2 md:px-4 md:py-2 rounded-full text-xs md:text-sm font-medium transition-all touch-target', 
                       activeFilter === 'all' ? 'bg-indigo-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200']">
              Tous
            </button>
            <button 
              @click="activeFilter = 'nouveau'"
              :class="['px-3 py-2 md:px-4 md:py-2 rounded-full text-xs md:text-sm font-medium transition-all touch-target', 
                       activeFilter === 'nouveau' ? 'bg-emerald-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200']">
              <i class="fas fa-star mr-1"></i>
              <span class="hidden sm:inline">Nouveautés</span>
              <span class="sm:hidden">Nouveau</span>
            </button>
            <button 
              @click="activeFilter = 'coupDeCoeur'"
              :class="['px-3 py-2 md:px-4 md:py-2 rounded-full text-xs md:text-sm font-medium transition-all touch-target', 
                       activeFilter === 'coupDeCoeur' ? 'bg-rose-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200']">
              <i class="fas fa-heart mr-1"></i>
              <span class="hidden sm:inline">Coups de cœur</span>
              <span class="sm:hidden">❤️</span>
            </button>
            <button 
              @click="activeFilter = 'promo'"
              :class="['px-3 py-2 md:px-4 md:py-2 rounded-full text-xs md:text-sm font-medium transition-all touch-target', 
                       activeFilter === 'promo' ? 'bg-amber-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200']">
              <i class="fas fa-tag mr-1"></i>
              Promo
            </button>
            <button 
              @click="activeFilter = 'wattpad'"
              :class="['px-3 py-2 md:px-4 md:py-2 rounded-full text-xs md:text-sm font-medium transition-all touch-target', 
                       activeFilter === 'wattpad' ? 'bg-blue-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200']">
              <i class="fab fa-wattpad mr-1"></i>
              Wattpad
            </button>
          </div>
          
          <!-- Recherche et tri responsive -->
          <div class="flex flex-col sm:flex-row gap-3 w-full">
            <div class="relative flex-1">
              <input 
                v-model="searchQuery"
                type="text" 
                placeholder="Rechercher..."
                class="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent text-sm md:text-base">
              <i class="fas fa-search absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400"></i>
            </div>
            
            <select v-model="sortBy" class="border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-indigo-500 focus:border-transparent text-sm md:text-base min-w-0 sm:min-w-[160px]">
              <option value="title">Par titre</option>
              <option value="author">Par auteur</option>
              <option value="category">Par catégorie</option>
            </select>
          </div>
        </div>
      </div>
    </section>

    <!-- Section principale des livres -->
    <main id="livres" class="max-w-7xl mx-auto px-3 sm:px-6 lg:px-8 py-6 md:py-12">
      <div class="text-center mb-8 md:mb-12">
        <h2 class="font-display text-2xl md:text-3xl lg:text-4xl font-bold text-gray-900 mb-3 md:mb-4">
          Notre sélection de livres
        </h2>
        <p class="text-base md:text-lg text-gray-600 max-w-2xl mx-auto px-4">
          Découvrez des histoires captivantes créées par des auteurs passionnés et talentueux
        </p>
        <div class="mt-4 md:mt-6 text-sm text-gray-500">
          {{ filteredBooks.length }} livre{{ filteredBooks.length > 1 ? 's' : '' }} trouvé{{ filteredBooks.length > 1 ? 's' : '' }}
        </div>
      </div>
      
      <!-- Grille des livres responsive optimisée -->
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4 md:gap-6">
        <TransitionGroup name="book" tag="div" class="contents">
          <BookCard
            v-for="(book, index) in filteredBooks"
            :key="book.title + index"
            :title="book.title"
            :description="book.description"
            :link="book.link"
            :images="book.images"
            :socials="book.socials"
            :author="book.author"
            :category="book.category"
            :nouveau="book.nouveau"
            :coupDeCoeur="book.coupDeCoeur"
            :promo="book.promo"
            class="fade-in-up hover-lift"
            :style="{ animationDelay: `${index * 100}ms` }"
            @openDetail="() => openBookDetail(book)"
          />
        </TransitionGroup>
      </div>
      
      <!-- Message si aucun livre trouvé -->
      <div v-if="filteredBooks.length === 0" class="text-center py-12 md:py-16 px-4">
        <div class="w-16 h-16 md:w-24 md:h-24 bg-gray-100 rounded-full flex items-center justify-center mx-auto mb-4 md:mb-6">
          <i class="fas fa-search text-gray-400 text-2xl md:text-3xl"></i>
        </div>
        <h3 class="text-lg md:text-xl font-semibold text-gray-900 mb-2">Aucun livre trouvé</h3>
        <p class="text-gray-600 mb-4 md:mb-6 text-sm md:text-base">Essayez de modifier vos filtres ou votre recherche</p>
        <button @click="resetFilters" class="btn-primary text-sm md:text-base">
          <i class="fas fa-refresh mr-2"></i>
          Réinitialiser les filtres
        </button>
      </div>
    </main>
    
    <!-- Section statistiques responsive -->
    <section class="bg-white py-8 md:py-16">
      <div class="max-w-7xl mx-auto px-3 sm:px-6 lg:px-8">
        <div class="grid grid-cols-2 md:grid-cols-5 gap-4 md:gap-6 lg:gap-8 text-center">
          <div class="space-y-1 md:space-y-2">
            <div class="text-xl md:text-2xl lg:text-3xl font-bold text-indigo-600">{{ books.length }}</div>
            <div class="text-gray-600 text-xs md:text-sm lg:text-base">Livres</div>
          </div>
          <div class="space-y-1 md:space-y-2">
            <div class="text-xl md:text-2xl lg:text-3xl font-bold text-emerald-600">{{ newBooksCount }}</div>
            <div class="text-gray-600 text-xs md:text-sm lg:text-base">Nouveautés</div>
          </div>
          <div class="space-y-1 md:space-y-2">
            <div class="text-xl md:text-2xl lg:text-3xl font-bold text-rose-600">{{ heartBooksCount }}</div>
            <div class="text-gray-600 text-xs md:text-sm lg:text-base">Coups de cœur</div>
          </div>
          <div class="space-y-1 md:space-y-2">
            <div class="text-xl md:text-2xl lg:text-3xl font-bold text-amber-600">{{ promoBooksCount }}</div>
            <div class="text-gray-600 text-xs md:text-sm lg:text-base">Promotions</div>
          </div>
          <div class="space-y-1 md:space-y-2 col-span-2 md:col-span-1">
            <div class="text-xl md:text-2xl lg:text-3xl font-bold text-blue-600">{{ wattpadBooksCount }}</div>
            <div class="text-gray-600 text-xs md:text-sm lg:text-base">Wattpad</div>
          </div>
        </div>
      </div>
    </section>
    
        <!-- Footer -->
    <Footer />

    <!-- Modal de détail du livre -->
    <BookDetailModal 
      :show="showBookDetail" 
      :book="selectedBook" 
      @close="closeBookDetail"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import Header from './components/Header.vue'
import BookCard from './components/BookCard.vue'
import Footer from './components/Footer.vue'
import BookDetailModal from './components/BookDetailModal.vue'

// Importation du fichier JSON
import booksData from './assets/authors.json'

// Variables réactives
const books = ref(booksData)
const activeFilter = ref('all')
const searchQuery = ref('')
const sortBy = ref('title')

// Variables pour le modal de détail
const showBookDetail = ref(false)
const selectedBook = ref({})

// Fonctions de filtrage et tri
const filteredBooks = computed(() => {
  let filtered = books.value.filter(book => {
    // Filtre par recherche
    const matchesSearch = searchQuery.value === '' || 
      book.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
      book.author.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
      book.category.toLowerCase().includes(searchQuery.value.toLowerCase())
    
    // Filtre par catégorie
    const matchesFilter = activeFilter.value === 'all' ||
      (activeFilter.value === 'nouveau' && book.nouveau) ||
      (activeFilter.value === 'coupDeCoeur' && book.coupDeCoeur) ||
      (activeFilter.value === 'promo' && book.promo) ||
      (activeFilter.value === 'wattpad' && book.wattpad)

    return matchesSearch && matchesFilter
  })
  
  // Tri
  return filtered.sort((a, b) => {
    switch (sortBy.value) {
      case 'title':
        return a.title.localeCompare(b.title)
      case 'author':
        return a.author.localeCompare(b.author)
      case 'category':
        return a.category.localeCompare(b.category)
      default:
        return 0
    }
  })
})

// Statistiques
const newBooksCount = computed(() => books.value.filter(book => book.nouveau).length)
const heartBooksCount = computed(() => books.value.filter(book => book.coupDeCoeur).length)
const promoBooksCount = computed(() => books.value.filter(book => book.promo).length)
const wattpadBooksCount = computed(() => books.value.filter(book => book.wattpad).length)

// Fonctions
const resetFilters = () => {
  activeFilter.value = 'all'
  searchQuery.value = ''
  sortBy.value = 'title'
}

// Fonctions pour le modal de détail
const openBookDetail = (book) => {
  selectedBook.value = { 
    ...book,
    // Ajout de données POC pour la démo
    releaseDate: book.releaseDate || '2024',
    completed: book.completed !== undefined ? book.completed : Math.random() > 0.5,
    extendedDescription: book.extendedDescription || 'Aucune description disponible.',
    pageCount: book.pageCount,
    language: book.language || 'Français',
    isbn: book.isbn,
    rating: book.rating,
    tags: book.tags
  }
  showBookDetail.value = true
}

const closeBookDetail = () => {
  showBookDetail.value = false
  selectedBook.value = {}
}
</script>

<style scoped>
.book-enter-active, .book-leave-active {
  transition: all 0.5s ease;
}

.book-enter-from, .book-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.book-move {
  transition: transform 0.5s ease;
}
</style>
