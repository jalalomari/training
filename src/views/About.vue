<template>
   <div class="px-8">
     <!-- provide values -->
     <PageContent :pageTitle="pageTitle" :pageDescription="pageDescription" />
   </div>
 </template>
 
 <script setup>
 import PageContent from '@/views/PageContent.vue';
 import { provide } from 'vue';
 
 const pageTitle = 'About';
 const pageDescription = 'This is the About page.';
 
 provide('pageTitle', pageTitle);
 provide('pageDescription', pageDescription);
 </script>
 