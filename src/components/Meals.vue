<template>
  <div class="grid grid-cols-1 md:grid-cols-3 p-8">
    <MealItem v-for="meal in meals" :key="meal.idMeal" :meal="meal" />
  </div>
</template>

<script setup>
import MealItem from "../components/MealItem.vue";

const { meals } = defineProps({
  meals: {
    type: Array,
    required: true,
    default: () => [],
  },
});
</script>

