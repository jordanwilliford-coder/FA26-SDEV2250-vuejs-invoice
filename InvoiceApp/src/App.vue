<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/">Invoice</RouterLink> |
      <RouterLink to="/about">About</RouterLink>
    </nav>
  </header>

  <RouterView />
</template>