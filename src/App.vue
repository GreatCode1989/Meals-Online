<template>
  <div class="bg-gray-100 h-full">
    <header class="bg-white shadow h-16 flex justify-between">
      <router-link :to="{ name: 'home' }"> Home </router-link>
      <div>
        <router-link to="/"> Searcch Meals </router-link>
        <router-link to="/"> Meals by Letter </router-link>
        <router-link to="/"> Meals by Ingredient </router-link>
      </div>
    </header>

    <main>
      <router-view></router-view>
    </main>
  </div>
</template>

<script setup></script>

<style scoped></style>
