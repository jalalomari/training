<!-- Props -->
<template>
    <div class="content d-flex flex-column flex-column-fluid pt-0 px-0 pb-0">
      <div class="card px-0 mt-3">
        <h1 class="text-primary fw-boldest">{{ pageTitle }}</h1>
        <p>{{ pageDescription }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    pageTitle: String,
    pageDescription: String
  });
  </script>
  