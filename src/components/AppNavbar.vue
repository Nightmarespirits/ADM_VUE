<template>
    <v-app-bar app>
      <v-app-bar-nav-icon @click="$emit('toggle-drawer')"></v-app-bar-nav-icon>
      <v-toolbar-title>Speed Wash S.A.</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Buscar"
        single-line
        hide-details
        class="mr-4"
      ></v-text-field>
      <v-btn to="/" text>Inicio</v-btn>
      <v-btn to="/about" text>Acerca De</v-btn>
      <v-btn @click="toggleTheme" icon>
        <v-icon>{{ isDark ? 'mdi-weather-sunny' : 'mdi-weather-night' }}</v-icon>
      </v-btn>
    </v-app-bar>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  import { useTheme } from 'vuetify';
  
  const theme = useTheme();
  const search = ref('');
  
  const isDark = computed(() => theme.global.current.value.dark);
  
  const toggleTheme = () => {
    theme.global.name.value = isDark.value ? 'light' : 'dark';
  };
  </script>