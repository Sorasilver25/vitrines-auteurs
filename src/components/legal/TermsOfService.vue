<template>
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
    <div class="bg-white rounded-xl shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-hidden">
      <!-- En-tête -->
      <div class="bg-gradient-to-r from-indigo-600 to-purple-600 text-white p-6">
        <div class="flex justify-between items-center">
          <div>
            <h2 class="text-2xl font-bold">Conditions d'Utilisation</h2>
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
            <h3 class="text-xl font-semibold text-gray-900 mb-4">1. Acceptation des Conditions</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              En accédant et en utilisant le site Vitrine Auteurs, vous acceptez de vous conformer aux présentes conditions d'utilisation. 
              Si vous n'acceptez pas ces conditions, veuillez ne pas utiliser ce site.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">2. Nature du Service</h3>
            <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 mb-4">
              <div class="flex items-center mb-2">
                <i class="fas fa-info-circle text-blue-600 mr-2"></i>
                <strong class="text-blue-800">Service Promotionnel Gratuit</strong>
              </div>
              <p class="text-blue-700">
                Vitrine Auteurs est un projet open source gratuit et communautaire destiné uniquement à la promotion de livres d'auteurs auto-édités.
              </p>
            </div>
            <ul class="list-disc list-inside text-gray-700 space-y-2">
              <li>Le site ne vend aucun produit directement</li>
              <li>Aucune transaction commerciale n'est effectuée sur le site</li>
              <li>Les liens vers les plateformes de vente sont fournis à titre informatif</li>
              <li>Le service est entièrement gratuit pour les visiteurs et les auteurs</li>
            </ul>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">3. Droits d'Auteur et Propriété Intellectuelle</h3>
            <div class="bg-amber-50 border border-amber-200 rounded-lg p-4 mb-4">
              <div class="flex items-center mb-2">
                <i class="fas fa-copyright text-amber-600 mr-2"></i>
                <strong class="text-amber-800">Respect de la Propriété Intellectuelle</strong>
              </div>
              <p class="text-amber-700">
                Tous les droits sur les œuvres présentées appartiennent exclusivement à leurs auteurs respectifs.
              </p>
            </div>
            <ul class="list-disc list-inside text-gray-700 space-y-2">
              <li>Les couvertures, titres et descriptions appartiennent aux auteurs</li>
              <li>Vitrine Auteurs ne revendique aucun droit sur les œuvres présentées</li>
              <li>L'utilisation des éléments promotionnels se fait avec l'accord des auteurs</li>
              <li>Toute violation de droits d'auteur sera immédiatement corrigée</li>
            </ul>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">4. Utilisation Acceptable</h3>
            <p class="text-gray-700 leading-relaxed mb-4">En utilisant ce site, vous vous engagez à :</p>
            <ul class="list-disc list-inside text-gray-700 space-y-2 mb-4">
              <li>Respecter les droits d'auteur et la propriété intellectuelle</li>
              <li>Ne pas utiliser le site à des fins illégales ou non autorisées</li>
              <li>Ne pas perturber le fonctionnement du site</li>
              <li>Respecter les autres utilisateurs et auteurs</li>
            </ul>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">5. Liens Externes</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Le site contient des liens vers des plateformes externes (Amazon, sites d'auteurs, réseaux sociaux). 
              Vitrine Auteurs n'est pas responsable du contenu, des politiques ou des pratiques de ces sites externes.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">6. Limitation de Responsabilité</h3>
            <div class="bg-gray-50 border border-gray-200 rounded-lg p-4 mb-4">
              <p class="text-gray-700">
                Vitrine Auteurs est fourni "en l'état" sans garanties d'aucune sorte. 
                Nous ne sommes pas responsables des dommages directs ou indirects résultant de l'utilisation du site.
              </p>
            </div>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">7. Ajout de Livres</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Les auteurs souhaitant ajouter leurs livres à la vitrine peuvent nous contacter. 
              L'ajout se fait gratuitement et reste à la discrétion de l'équipe du projet.
            </p>
            <ul class="list-disc list-inside text-gray-700 space-y-2">
              <li>Aucun frais n'est demandé pour l'ajout d'un livre</li>
              <li>L'auteur conserve tous ses droits sur son œuvre</li>
              <li>L'auteur peut demander le retrait de son livre à tout moment</li>
            </ul>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">8. Modifications des Conditions</h3>
            <p class="text-gray-700 leading-relaxed mb-4">
              Ces conditions peuvent être modifiées à tout moment. Les modifications seront publiées sur cette page 
              avec une nouvelle date de mise à jour.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">9. Contact</h3>
            <p class="text-gray-700 leading-relaxed">
              Pour toute question concernant ces conditions d'utilisation, contactez-nous via Instagram : 
              <a href="https://instagram.com/evil._night._" target="_blank" class="text-indigo-600 hover:text-indigo-800 underline">
                @evil._night._
              </a>
            </p>
          </section>
        </div>
      </div>
      
      <!-- Pied de page -->
      <div class="bg-gray-50 px-6 py-4 border-t">
        <div class="flex justify-between items-center">
          <div class="text-sm text-gray-500">
            Conditions pour un projet open source communautaire
          </div>
          <button @click="$emit('close')" class="btn-primary">
            J'accepte
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
