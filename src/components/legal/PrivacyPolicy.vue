<template>
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
    <div class="bg-white rounded-xl shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-hidden">
      <!-- En-tête -->
      <div class="bg-gradient-to-r from-indigo-600 to-purple-600 text-white p-6">
        <div class="flex justify-between items-center">
          <div>
            <h2 class="text-2xl font-bold">Politique de Confidentialité</h2>
            <p class="text-indigo-100 mt-1">Vitrine Auteurs - Projet Open Source</p>
          </div>
          <button @click="$emit('close')" 
                  class="w-8 h-8 bg-white bg-opacity-20 hover:bg-opacity-30 rounded-full flex items-center justify-center transition-all">
            <i class="fas fa-times"></i>
          </button>
        </div>
      </div>
      
      <!-- Contenu -->
      <div class="p-6 overflow-y-auto max-h-[calc(90vh-120px)]">
        <div class="prose max-w-none">
          <p class="text-gray-600 mb-6">Dernière mise à jour : {{ currentDate }}</p>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">1. Nature du Projet</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Vitrine Auteurs est un projet <strong>open source gratuit et communautaire</strong> dédié à la promotion des livres d'auteurs auto-édités. 
              Ce site fonctionne uniquement à titre promotionnel et ne collecte aucune donnée personnelle des visiteurs.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">2. Absence de Collecte de Données</h3>
            <div class="bg-green-50 border border-green-200 rounded-lg p-4 mb-4">
              <div class="flex items-center mb-2">
                <i class="fas fa-shield-alt text-green-600 mr-2"></i>
                <strong class="text-green-800">Votre vie privée est totalement respectée</strong>
              </div>
              <p class="text-green-700">
                Ce site ne collecte, ne stocke et ne traite aucune donnée personnelle des visiteurs.
              </p>
            </div>
            <ul class="list-disc list-inside text-gray-700 space-y-2">
              <li>Aucun cookie de tracking</li>
              <li>Aucun formulaire de contact collectant des données</li>
              <li>Aucune analyse comportementale</li>
              <li>Aucun stockage d'informations personnelles</li>
              <li>Aucune revente de données (puisqu'il n'y en a pas)</li>
            </ul>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">3. Liens Externes</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Ce site contient des liens vers des plateformes externes (Amazon, sites d'auteurs, réseaux sociaux). 
              Ces plateformes ont leurs propres politiques de confidentialité que nous vous encourageons à consulter.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">4. Hébergement et Sécurité</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Le site est hébergé de manière sécurisée. Étant donné l'absence de collecte de données, 
              il n'y a aucun risque de fuite d'informations personnelles.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">5. Droits des Visiteurs</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Puisque nous ne collectons aucune donnée personnelle, il n'y a aucune information vous concernant à 
              consulter, modifier ou supprimer. Votre anonymat est total lors de votre navigation.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">6. Contact</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Pour toute question concernant cette politique de confidentialité, vous pouvez nous contacter via Instagram : 
              <a href="https://instagram.com/evil._night._" target="_blank" class="text-indigo-600 hover:text-indigo-800 underline">
                @evil._night._
              </a>
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">7. Modifications</h3>
            <p class="text-gray-700 leading-relaxed">
              Cette politique peut être mise à jour pour refléter des changements dans nos pratiques. 
              Toute modification sera publiée sur cette page avec une nouvelle date de mise à jour.
            </p>
          </section>
        </div>
      </div>
      
      <!-- Pied de page -->
      <div class="bg-gray-50 px-6 py-4 border-t">
        <div class="flex justify-between items-center">
          <div class="text-sm text-gray-500">
            Document généré automatiquement pour un projet open source
          </div>
          <button @click="$emit('close')" class="btn-primary">
            J'ai compris
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineEmits(['close'])

const currentDate = ref(new Date().toLocaleDateString('fr-FR', { 
  year: 'numeric', 
  month: 'long', 
  day: 'numeric' 
}))
</script>
