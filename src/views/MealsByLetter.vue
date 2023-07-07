<template>
  <div class="flex justify-center gap-2 mt-2">
    <router-link
      v-for="letter of letters"
      :key="letter"
      :to="{ name: 'byLetter', params: { letter } }"
      @click="handleLetterClick(letter)"
    >
      {{ letter }}
    </router-link>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";

const route = useRoute();
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter);

function handleLetterClick(letter) {
  store.dispatch("searchMealsByLetter", letter);
}

onMounted(() => {
  const letter = route.params.letter;
  if (letter) {
    store.dispatch("searchMealsByLetter", letter);
  }
});
</script>
