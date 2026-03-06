<script setup>
import { ref, computed } from 'vue'
import home from './home.vue'
import bookclubs from './bookclubs.vue'
import audiobooks from './audiobooks.vue'
import library from './library.vue'
import order from './order.vue'

const routes = {
  '/': home,
  '/bookclubs': bookclubs,
  '/audiobooks': audiobooks,
  '/library': library,
  '/order': order,
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
    <v-navigation-drawer
        v-model="drawer"
        color="#FFFFFF"
        elevation="2"
        class="drawer-font">
      <v-list-item prepend-icon="mdi-home" href="#/" title="Home" @click="drawer = !drawer"></v-list-item>
      <v-list-item prepend-icon="mdi-bookshelf" href="#/bookclubs" title="Book Clubs" @click="drawer = !drawer"/>
<!--      <v-list-item prepend-icon="mdi-book-music" href="#/audiobooks" title="Audiobooks" @click="drawer = !drawer"/>-->
      <v-list-item prepend-icon="mdi-book-multiple" href="#/library" title="My Shelf" @click="drawer = !drawer"/>
<!--      <v-list-item prepend-icon="mdi-receipt-text-check-outline" href="#/order" title="Place an Order" @click="drawer = !drawer"/>-->
    </v-navigation-drawer>

    <v-app-bar color="white" elevation="2">
      <v-app-bar-nav-icon color="#1a2a44" @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-app-bar-title style="font-family:'Playfair Display', serif; font-weight:700; color:#1a2a44;">
        Shelf Life
      </v-app-bar-title>
    </v-app-bar>

    <v-main>
      <component :is="currentView"></component>
    </v-main>

    <v-footer color="#FFFFFF" class="text-center" elevation="1">
      <span style="color:#1a2a44;">
        <v-icon start>mdi-copyright</v-icon>
        2026 Megan Grow</span>
    </v-footer>
  </v-app>
</template>

<style scoped>
</style>