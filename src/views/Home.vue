<template>
  <div class="flex flex-col p-8">
    <input
      type="text"
      class="rounded border-2 border-gray-200 w-full"
      placeholder="Search for Meals"
    />
  </div>
  <div>
    <router-link
      :to="{
        name: 'byIngredient',
        params: { ingredient: ingredient.strIngredient },
      }"
      v-for="ingredient of randomMeals"
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
import { onMounted } from "vue";
import { ref } from "vue";
import axiosClient from "../AxiosClient";

const ingredients = ref([]);
const randomMeals = ref([]);

onMounted(async () => {
  const response = await axiosClient.get("/list.php?i=list");
  ingredients.value = response.data.meals;

  // Выбор случайных блюд
  const numRandomMeals = 5; // Количество случайных блюд, которые нужно отобразить
  const randomIndices = getRandomIndices(
    ingredients.value.length,
    numRandomMeals
  );
  randomMeals.value = randomIndices.map((index) => ingredients.value[index]);
});

// Функция для генерации случайных индексов
function getRandomIndices(max, count) {
  const indices = [];
  while (indices.length < count) {
    const randomIndex = Math.floor(Math.random() * max);
    if (!indices.includes(randomIndex)) {
      indices.push(randomIndex);
    }
  }
  return indices;
}
</script>
