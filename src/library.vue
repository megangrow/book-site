<script setup>
import { onMounted, ref, computed } from 'vue'
import Book from './components/book.vue'

const books = ref([])
const loading = ref(true)
const error = ref('')
const path = '/api/library'
// const path = 'http://localhost:3000/library'

async function loadBooks() {
  loading.value = true
  error.value = ''

  try {
      const response = await fetch(path)
      if (!response.ok) {
        throw new Error('Failed to load books')
      }
      const data = await response.json()
      books.value = data

  } catch (err) {
    error.value = err.message || 'Something went wrong while loading'
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  loadBooks()
})

async function changeShelf(book, newShelf) {
  console.log("here!")
  try {
    await fetch(path, {
      method: 'PATCH',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ id: book.id, shelf: newShelf })
    })
    book.shelf = newShelf

  } catch (err) {
    error.value = err.message
  }
}

const dialogOpen = ref(false)
const selectedBook = ref(null)
function openDetails(book) {
  selectedBook.value = book
  dialogOpen.value = true
}

const pageSize = 4

function chunkedBooks(arr) {
  const chunks = []
  for (let i = 0; i < arr.length; i += pageSize) {
    chunks.push(arr.slice(i, i + pageSize))
  }
  return chunks
}

const ReadingChunks = computed(() => chunkedBooks(books.value.filter(b => b.shelf === 'Reading')))
const ReadChunks = computed(() => chunkedBooks(books.value.filter(b => b.shelf === 'Read')))
const TBRChunks = computed(() => chunkedBooks(books.value.filter(b => b.shelf === 'TBR')))
</script>

<template>
  <div class="hero">
    <h1>My Shelf</h1>
    <p>View all your saved books here!</p>
  </div>

  <div class="shelf-section">
  <h2>Currently Reading</h2>
    <v-carousel v-if="!loading" hide-delimiter-background hide-delimiters continuous height="400" :show-arrows="false">
      <v-carousel-item
        v-for="(group, index) in ReadingChunks"
        :key="index"
    >
      <div class="carousel-slide">
        <Book
            v-for="book in group"
            :key="book.id"
            :title="book.title"
            :author="book.author"
            :image="book.image"
            :description="book.description"
            @view-details="openDetails(book)"
        />
      </div>
    </v-carousel-item>
  </v-carousel>
  </div>

  <div class="shelf-section">
    <h2>Past Reads</h2>
    <v-carousel v-if="!loading" hide-delimiter-background hide-delimiters continuous height="400">
      <v-carousel-item
        v-for="(group, index) in ReadChunks"
        :key="index"
    >
      <div class="carousel-slide">
        <Book
            v-for="book in group"
            :key="book.title"
            :title="book.title"
            :author="book.author"
            :image="book.image"
            :description="book.description"
            @view-details="openDetails(book)"
        />
      </div>
    </v-carousel-item>
  </v-carousel>
  </div>

  <div class="shelf-section">
    <h2>To Be Read</h2>
    <v-carousel v-if="!loading" hide-delimiter-background hide-delimiters continuous height="400">
    <v-carousel-item
        v-for="(group, index) in TBRChunks"
        :key="index"
    >
      <div class="carousel-slide">
        <Book
            v-for="book in group"
            :key="book.title"
            :title="book.title"
            :author="book.author"
            :image="book.image"
            :description="book.description"
            @view-details="openDetails(book)"
        />
      </div>
    </v-carousel-item>
  </v-carousel>
  </div>

  <v-dialog v-model="dialogOpen" max-width="600">
    <v-card v-if="selectedBook">
      <v-img :src="selectedBook.image" height="250" cover></v-img>
      <v-card-title>{{ selectedBook.title }}</v-card-title>
      <v-card-subtitle>{{ selectedBook.author }}</v-card-subtitle>

      <v-card-text>
        <v-chip
            v-for="chip in selectedBook.chips"
            :key="chip"
            class="chipp"
        >
          {{ chip }}
        </v-chip>
        <v-select
            v-model="selectedBook.shelf"
            :items="['Reading', 'Read', 'TBR']"
            label="Move to shelf"
            density="compact"
            variant="outlined"
            style="margin-top: 20px; margin-bottom: 16px;"
            hide-details
            @update:modelValue="changeShelf(selectedBook, $event)"
        />
        {{ selectedBook.description }}
      </v-card-text>

      <v-card-actions>
        <v-btn color="pink-darken-2" @click="dialogOpen = false">Close</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<style scoped>
.shelf-section {
  background-color: #001f5b; /* navy */
  color: white;
  padding: 2rem 1rem;
  margin-bottom: 2rem;
  border-radius: 8px;
  text-align: center; /* centers the title */
}

/* Shelf title */
.shelf-section h2 {
  color: white;
  margin-bottom: 1.5rem;
}

/* Carousel slides */
.carousel-slide {
  display: flex;
  justify-content: center;
  gap: 20px;
}
.chipp {
  background-color: #1a2a44;
  color: #fff;
  padding: 6px 12px;      /* vertical | horizontal padding */
  margin: 4px 4px 0 0;    /* top, right, bottom, left spacing between chips */
  border-radius: 16px;    /* rounded pill shape */
  font-size: 0.8rem;      /* optional: make text slightly smaller */
}

</style>