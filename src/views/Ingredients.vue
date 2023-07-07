<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-orange-400">Ingredient</h1>
    <input
      type="text"
      v-model="searchQuery"
      class="rounded border-2 border-gray-200 w-full mb-3 placeholder-blue-500"
      placeholder="Search for Ingredients"
      @input="searchIngredients"
    />
    <router-link
      :to="{
        name: 'byIngredient',
        params: { ingredient: ingredient.strIngredient },
      }"
      v-for="ingredient of filteredIngredients"
      :key="ingredient.idIngredient"
      class="block bg-white p-3 rounded mb-3 shadow"
    >
      <h3 class="text-2xl font-bold mb-2 text-orange-400">
        {{ ingredient.strIngredient }}
      </h3>
      <p>{{ ingredient.strDescription }}</p>
    </router-link>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import axiosClient from "../AxiosClient";
import { computed } from "vue";

const filteredIngredients = computed(() => {
  if (!searchQuery.value) {
    return ingredients.value;
  }

  const query =
    searchQuery.value !== null && searchQuery.value !== undefined
      ? searchQuery.value.toLowerCase()
      : "";
  return ingredients.value.filter(
    (ingredient) =>
      ingredient.strIngredient &&
      ingredient.strIngredient.toLowerCase().includes(query.toLowerCase())
  );
});

function searchIngredients() {
  const query = searchQuery.value.toLowerCase();

  if (!query) {
    filteredIngredients.value = ingredients.value;
    return;
  }

  filteredIngredients.value = ingredients.value.filter(
    (ingredient) =>
      ingredient.strIngredient &&
      ingredient.strIngredient.toLowerCase().includes(query.toLowerCase())
  );
}

const searchQuery = ref("");
const ingredients = ref([]);

onMounted(() => {
  axiosClient.get("list.php?i=list").then((response) => {
    const data = response.data;
    ingredients.value = data.meals;
  });
});
</script>
