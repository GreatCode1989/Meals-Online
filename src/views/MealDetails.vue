<template>
  <div>
    <pre>{{ meal }}</pre>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../AxiosClient";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then((data) => {
    debugger;
    meal.value = data;
  });
});
</script>

