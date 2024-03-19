<template>
  <div class="footer py-4 position-fixed w-100 bottom-0">
    <div class="container-fluid d-flex px-2">
      <div class="text-dark order-2 order-md-1 mx-1">
        <router-link v-for="(link, index) in routerLinks" :to="link.to" :key="index" class="text-decoration-underline text-dark px-3">{{ link.text }}</router-link>
      </div>
      <ul class="text-gray-800 order-1 mb-0 px-5 fw-boldest">
        <li v-for="(item, index) in footerItems" :key="index" class="d-inline">{{ item }}</li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router';

const footerItems = ["Aumet Inc", " | ", "2024 © All Rights Reserved"];

const routerLinks = [
  { to: '/home', text: 'Home' },
  { to: '/about', text: 'About' }
];
</script>

<style scoped>

</style>
