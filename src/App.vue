<script setup>
import { ref, computed } from 'vue'
import home from './home.vue'
import library from './library.vue'
import audiobooks from './audiobooks.vue'
import journey from './journey.vue'

const routes = {
  '/': home,
  '/library': library,
  '/audiobooks': audiobooks,
  '/journey': journey
}

const currentPath = ref(window.location.hash)
const drawer = ref(false)

window.addEventListener('hashchange', ()=> {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/' || NotFound]
})
</script>

<template>
  <v-app>
    <v-navigation-drawer class="text-deep-purple-darken-3" color="purple-lighten-3"v-model="drawer">
      <v-list-item prepend-icon="mdi-home" href="#/" title="Home" @click="drawer = !drawer"></v-list-item>
      <v-list-item prepend-icon="mdi-bookshelf" href="#/library" title="Library" @click="drawer = !drawer"></v-list-item>
      <v-list-item prepend-icon="mdi-book-music" href="#/audiobooks" title="Audiobooks" @click="drawer = !drawer"></v-list-item>
      <v-list-item prepend-icon="mdi-progress-star" href="#/journey" title="My Journey" @click="drawer = !drawer"></v-list-item>
    </v-navigation-drawer>
    <v-app-bar class="text-deep-purple-darken-3" color="purple-lighten-3" height="100">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title>Book Website</v-app-bar-title>
    </v-app-bar>
    <v-main>
      <component :is="currentView"></component>
    </v-main>
    <v-footer app="true">Copyright 2026</v-footer>
  </v-app>
</template>

<style scoped>
* {
  font-family: "Red Hat Text", sans-serif;
  font-optical-sizing: auto;
  font-style: normal;
  line-height: 1.6;
}
</style>