<template>
  <a
    v-if="href"
    :href="href"
    target="_blank"
    class="px-3 py-2 rounded-xl bg-red-700 text-white hover:bg-red-500 hover:text-white transition-colors"
  >
    <slot></slot>
  </a>
  <span v-else class="text-red-400">
    YouTube not accepted Request for this dish!</span
  >
</template>

<script setup>
const props = defineProps({ href: String });
</script>

