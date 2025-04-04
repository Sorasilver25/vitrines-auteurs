<template>
  <div class="min-h-screen bg-white text-gray-800">
    <Header />
    <main class="p-4 max-w-4xl mx-auto">
      <h1 class="text-3xl font-bold mb-4">Bienvenue sur la vitrine des auteurs auto-édités</h1>
      
      <div v-for="(book, index) in books" :key="index">
        <BookCard
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
        />
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import BookCard from './components/BookCard.vue'

// Importation du fichier JSON
import booksData from './assets/authors.json'

// Stockage des livres dans une variable réactive
const books = ref(booksData)
</script>
