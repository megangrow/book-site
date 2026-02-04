<script setup>
import { ref, computed } from 'vue'
import home from './home.vue'
import Library from './library.vue'
import audiobooks from './audiobooks.vue'

const routes = {
  '/': home,
  '/library': Library,
  '/audiobooks': audiobooks
}

const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', ()=> {
  currentPath.value = window.location.hash
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/' || NotFound]
})
</script>

<template>
  <a href="#/">Home</a>
  <a href="#/library">Library</a>
  <a href="#/audiobooks">Audiobooks</a>

  <component :is="currentView"></component>
</template>