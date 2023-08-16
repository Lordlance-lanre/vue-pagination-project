<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
   <nav class="flex justify-evenly mt-2 mb-7">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
  <RouterView />
</template>

