<template>
  <div>
    <template v-if="!isLoginRoute">
      <layout />
    </template>
    <router-view v-if="isLoginRoute" />
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router';
import { computed } from 'vue';
import layout from './components/layout/Layout.vue';

const route = useRoute();
const isLoginRoute = computed(() => route.name === 'login');
</script>
