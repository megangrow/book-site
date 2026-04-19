<script setup>
import { ref, onMounted, computed } from 'vue'
const books = ref([])

onMounted(async () => {
const response = await fetch('http://localhost:3000/library')
books.value = await response.json()
})

const highlights = computed(() => books.value.filter(b => b.highlight === 1))
const currents = computed(() => books.value.filter(b => b.shelf === 'Reading'))
</script>

<template>
  <div class="hero">
    <h1>Featured Books of April</h1>
    <p>Books that our shelf scouts found profound this month. </p>
  </div>

  <v-card class="book-card" v-for="item in highlights" :key="item.title" cols="12" sm="6" md="4">
    <div class="top-banner">
      <v-icon>mdi-heart-circle</v-icon>
      April Favorite
      <v-icon>mdi-heart-circle</v-icon>
    </div>

    <v-row align="center">
      <v-col cols="3">
        <v-img :src="item.image" height="220" cover/>
      </v-col>

    <v-col cols="6">
      <v-card-title>{{ item.title }}</v-card-title>
      <v-card-subtitle>{{ item.author }}</v-card-subtitle>
      <v-card-text>{{ item.description }}</v-card-text>

      <div class="chips">
        <v-chip v-if="item.shelf === 'Reading'" class="my-shelf-chip"> My Shelf </v-chip>
        <v-chip v-for="chip in item.chips" :key="item.chip">{{ chip }}</v-chip>
      </div>
    </v-col>
    </v-row>
  </v-card>
</template>

<style scoped>


.book-card {
  border-radius: 16px;
  background-color: #FFFFFF;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
  transition: all 0.2s ease;
  margin-bottom: 3rem;
}

.book-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.08);
}

.chips {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}

v-chip {
  color: #1a2a44;
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
}

.my-shelf-chip {
  background-color: #1a2a44;
  color: #FFFFFF;
}

.top-banner {
  width: 100%;
  background-color: #C8A2C8;
  color: white;
  font-family: 'Playfair Display', serif;
  font-weight: 700;
  font-size: 1rem;
  text-align: center;
  padding: 0.5rem 0;
  border-top-left-radius: 16px;
  border-top-right-radius: 16px;
}
</style>