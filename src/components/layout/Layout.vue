<template>
    <div class="app d-flex">
      <!-- Sidebar -->
      <Sidebar />
      <main class="p-0 w-100">
        <!-- header -->
        <header>
          <Header />
        </header>
        <!-- RouterView -->
        <router-view />
        <!-- footer -->
        <footer>
          <Footer />
        </footer>
      </main>
    </div>
  </template>
  
  <script setup>
  import { RouterView } from 'vue-router';
  import Header from '@/components/header/Header.vue';
  import Footer from '@/components/footer/Footer.vue';
  import Sidebar from '@/components/menu/Sidebar.vue';
  </script>
  
 