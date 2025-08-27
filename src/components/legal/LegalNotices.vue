<template>
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
    <div class="bg-white rounded-xl shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-hidden">
      <!-- En-tête -->
      <div class="bg-gradient-to-r from-indigo-600 to-purple-600 text-white p-6">
        <div class="flex justify-between items-center">
          <div>
            <h2 class="text-2xl font-bold">Mentions Légales</h2>
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
            <h3 class="text-xl font-semibold text-gray-900 mb-4">1. Identification du Site</h3>
            <div class="bg-indigo-50 border border-indigo-200 rounded-lg p-4 mb-4">
              <ul class="text-gray-700 space-y-2">
                <li><strong>Nom du site :</strong> Vitrine Auteurs</li>
                <li><strong>Type :</strong> Projet open source gratuit et communautaire</li>
                <li><strong>Objet :</strong> Promotion de livres d'auteurs auto-édités</li>
                <li><strong>Contact :</strong> <a href="https://instagram.com/evil._night._" target="_blank" class="text-indigo-600 hover:text-indigo-800 underline">@evil._night._</a> (Instagram)</li>
              </ul>
            </div>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">2. Nature du Projet</h3>
            <div class="bg-green-50 border border-green-200 rounded-lg p-4 mb-4">
              <div class="flex items-center mb-2">
                <i class="fas fa-heart text-green-600 mr-2"></i>
                <strong class="text-green-800">Projet Communautaire et Gratuit</strong>
              </div>
              <p class="text-green-700 mb-2">
                Vitrine Auteurs est un projet open source entièrement gratuit, développé par passion pour soutenir les auteurs auto-édités.
              </p>
              <ul class="text-green-700 space-y-1">
                <li>• Aucun but lucratif</li>
                <li>• Aucune commission sur les ventes</li>
                <li>• Service promotionnel gratuit</li>
                <li>• Code source ouvert</li>
              </ul>
            </div>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">3. Propriété Intellectuelle</h3>
            <div class="bg-amber-50 border border-amber-200 rounded-lg p-4 mb-4">
              <h4 class="font-semibold text-amber-800 mb-2">Droits des Auteurs</h4>
              <p class="text-amber-700 mb-2">
                <strong>Tous les droits sur les œuvres présentées appartiennent exclusivement à leurs auteurs respectifs.</strong>
              </p>
              <ul class="text-amber-700 space-y-1">
                <li>• Couvertures de livres : © Auteurs respectifs</li>
                <li>• Titres et descriptions : © Auteurs respectifs</li>
                <li>• Contenus promotionnels : utilisés avec autorisation</li>
              </ul>
            </div>
            
            <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
              <h4 class="font-semibold text-blue-800 mb-2">Code du Site</h4>
              <p class="text-blue-700">
                Le code source de ce site est disponible sous licence open source. 
                Seuls les éléments techniques du site sont concernés, pas les contenus des auteurs.
              </p>
            </div>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">4. Responsabilité</h3>
            <div class="space-y-4">
              <div>
                <h4 class="font-semibold text-gray-800 mb-2">Contenu des Œuvres</h4>
                <p class="text-gray-700">
                  Les auteurs sont seuls responsables du contenu de leurs œuvres. 
                  Vitrine Auteurs n'exerce aucun contrôle éditorial sur les livres présentés.
                </p>
              </div>
              
              <div>
                <h4 class="font-semibold text-gray-800 mb-2">Liens Externes</h4>
                <p class="text-gray-700">
                  Les liens vers des plateformes de vente ou sites d'auteurs sont fournis à titre informatif. 
                  Nous ne sommes pas responsables du contenu de ces sites externes.
                </p>
              </div>
              
              <div>
                <h4 class="font-semibold text-gray-800 mb-2">Disponibilité du Service</h4>
                <p class="text-gray-700">
                  Bien que nous nous efforcions de maintenir le site accessible, 
                  nous ne garantissons pas une disponibilité 24h/24.
                </p>
              </div>
            </div>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">5. Protection des Données</h3>
            <div class="bg-green-50 border border-green-200 rounded-lg p-4">
              <div class="flex items-center mb-2">
                <i class="fas fa-shield-alt text-green-600 mr-2"></i>
                <strong class="text-green-800">Aucune Collecte de Données</strong>
              </div>
              <p class="text-green-700">
                Ce site ne collecte, ne stocke et ne traite aucune donnée personnelle des visiteurs. 
                Votre navigation est totalement anonyme.
              </p>
            </div>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">6. Droit Applicable</h3>
            <p class="text-gray-700 leading-relaxed">
              Ce site étant un projet open source international à but non lucratif, 
              les présentes mentions légales sont régies par les principes généraux du droit d'auteur 
              et de la propriété intellectuelle reconnus internationalement.
            </p>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">7. Signalement</h3>
            <div class="bg-red-50 border border-red-200 rounded-lg p-4">
              <p class="text-red-700 mb-2">
                <strong>En cas de problème de droits d'auteur ou de contenu inapproprié :</strong>
              </p>
              <p class="text-red-700">
                Contactez-nous immédiatement via Instagram : 
                <a href="https://instagram.com/evil._night._" target="_blank" class="underline">@evil._night._</a>
              </p>
              <p class="text-red-600 text-sm mt-2">
                Toute violation signalée sera traitée dans les plus brefs délais.
              </p>
            </div>
          </section>
          
          <section class="mb-8">
            <h3 class="text-xl font-semibold text-gray-900 mb-4">8. Modifications</h3>
            <p class="text-gray-700 leading-relaxed">
              Ces mentions légales peuvent être mises à jour pour refléter l'évolution du projet. 
              Toute modification sera publiée sur cette page avec une nouvelle date de mise à jour.
            </p>
          </section>
        </div>
      </div>
      
      <!-- Pied de page -->
      <div class="bg-gray-50 px-6 py-4 border-t">
        <div class="flex justify-between items-center">
          <div class="text-sm text-gray-500">
            Mentions légales d'un projet open source communautaire
          </div>
          <button @click="$emit('close')" class="btn-primary">
            Fermer
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
