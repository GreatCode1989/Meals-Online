<template>
  <Meals :meals="meals" />
</template>

<script setup>
import { onMounted, computed } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";

const route = useRoute();
const meals = computed(() => store.state.mealsByIngredient);

onMounted(() => {
  store.dispatch("searchMealsByIngredients", route.params.ingredient);
  console.log(store.state.mealsByIngredient);
});
</script>
