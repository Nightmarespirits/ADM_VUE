<template>
  <v-app>
    <AppSidebar v-model="drawer" />
    <AppNavbar @toggle-drawer="drawer = !drawer" />
    <v-main>
      <router-view />
    </v-main>
    <AppFooter />
  </v-app>
</template>

<script setup>
import AppNavbar from '@/components/AppNavbar.vue';
import AppSidebar from '@/components/AppSidebar.vue';
import { ref } from 'vue';

const drawer = ref(null);
  //
</script>
