<template>
    <!-- inject value -->
    <div class="content d-flex flex-column flex-column-fluid pt-0 px-0 pb-0">
      <div class="card p-4 mt-3">
        <h1 class="text-primary fw-boldest">{{ injectedPageTitle }}</h1>
        <p>{{ injectedPageDescription }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { inject } from 'vue';
  
  const injectedPageTitle = inject('pageTitle');
  const injectedPageDescription = inject('pageDescription');
  </script>
  