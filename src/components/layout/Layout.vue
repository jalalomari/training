<template>
    <div class="app">
      <!-- Sidebar -->
      <Sidebar />
      <main>
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
  
  <script setup lang="ts">
  import { RouterView } from 'vue-router';
  import Header from '@/components/header/Header.vue';
  import Footer from '@/components/footer/Footer.vue';
  import Sidebar from '@/components/menu/Sidebar.vue';
  </script>
  
  <style >
  button {
      cursor: pointer;
      appearance: none;
      border: none;
      outline: none;
      background: none;
  }
  .app {
    display: flex;
  }
  
  .app main {
    flex: 1 1 0;
    padding: 0px;
  }
  </style>