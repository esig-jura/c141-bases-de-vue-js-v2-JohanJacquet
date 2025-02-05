<template>
  <v-container max-width="700">
    <!-- Donnée de l'exercice -->
    <exercice-objectifs number="5" />
    <!-- Zone de travail pour l'exercice -->
    <div class="exe-zone">
      <h2>Zone d'exercice</h2>
      <v-card class="mx-auto my-6 pa-2" max-width="500">
        <v-card-title>Saisie surveillée</v-card-title>

        <v-card-text>
          <v-alert v-show="containsPokemon" type="success" class="mb-2">
            Vous avez mentionné "Pokémon" !
          </v-alert>

          <v-text-field
            v-model="userInput"
            label="Tapez quelque chose"
            placeholder="Essayez d'écrire Pokémon"
            outlined
          />

          <v-card-subtitle>
            Nombre de caractères :
            {{ charCount }}
          </v-card-subtitle>
        </v-card-text>
      </v-card>
    </div>
  </v-container>
</template>

<script setup>
// Importation du composant contenant la donnée de l'exerciced
import ExerciceObjectifs from "@/components/ExerciceObjectifs.vue";
// Importation de la fonction réactive ref
import { ref, watch, computed } from 'vue';

const MAX_LENGTH = 20;

// Variable réactive pour la saisie utilisateur
const userInput = ref('');

const charCount = computed(() => userInput.value.length);

const containsPokemon = ref(false);

watch(userInput, () => {
  if (MAX_LENGTH === userInput.value.length) {
    userInput.value = ''
  }

  if (userInput.value.toUpperCase().indexOf("POKEMON") === -1) {
    containsPokemon.value = false;
  } else {
    containsPokemon.value = true;
  }

})
</script>
