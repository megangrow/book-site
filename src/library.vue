<script setup>
import { ref, computed } from 'vue'
import Book from './components/book.vue'
import ClubCard from "@/components/clubCard.vue";

const books = ref([
  {
    title: "The Martian",
    author: "Andy Weir",
    description: "The Martian follows astronaut Mark Watney as he uses science, ingenuity, and humor to survive alone on Mars after being mistakenly left behind by his crew.",
    image: "book_1.jpg",
    chips: ["Science Fiction", "Adventure"],
    shelf: "TBR",
  },
  {
    title: "Sunrise on the Reaping",
    author: "Suzanne Collins",
    description: "A Hunger Games prequel set during the 50th Games, exploring the world of Panem and the forces that shaped its rebellion.",
    image: "book_5.jpg",
    chips: ["Dystopian", "Adventure"],
    shelf: "TBR",
  },
  {
    title: "Pride and Prejudice",
    author: "Jane Austen",
    description: "A classic romantic novel following Elizabeth Bennet as she navigates manners, marriage, morality, and misunderstandings in Regency England.",
    image: "book_6.jpg",
    chips: ["Romance", "Classic"],
    shelf: "TBR",
  },
  {
    title: "Little Women",
    author: "Louisa May Alcott",
    description: "The beloved story of the four March sisters as they grow up, face hardships, and discover their own paths in life.",
    image: "book_7.jpg",
    chips: ["Classic", "Coming of Age"],
    shelf: "TBR",
  },
  {
    title: "Lessons in Chemistry",
    author: "Bonnie Garmus",
    description: "A brilliant chemist in the 1960s unexpectedly becomes the star of a cooking show, challenging societal expectations for women.",
    image: "book_8.jpg",
    chips: ["Historical Fiction", "Humor"],
    shelf: "TBR",
  },
  {
    title: "The Book of Lost Names",
    author: "Kristin Harmel",
    description: "During World War II, a young Jewish woman forges documents for children escaping the Nazis while secretly encoding their real identities.",
    image: "book_9.jpg",
    chips: ["Historical Fiction", "War"],
    shelf: "TBR",
  },
  {
    title: "Mr. Lemoncello's Library",
    author: "Chris Grabenstein",
    description: "A group of kids compete in a puzzle-filled overnight adventure inside the world's most imaginative library.",
    image: "book_10.jpg",
    chips: ["Adventure", "Mystery"],
    shelf: "TBR",
  },
  {
    title: "Project Hail Mary",
    author: "Andy Weir",
    description: "A lone astronaut wakes up in space with no memory and must save Earth from an extinction-level threat.",
    image: "book_11.jpg",
    chips: ["Science Fiction", "Space"],
    shelf: "TBR",
  },
  {
    title: "The Night Circus",
    author: "Erin Morgenstern",
    description: "Two young magicians compete in a mysterious magical duel inside a traveling circus that appears only at night.",
    image: "book_12.jpg",
    chips: ["Fantasy", "Romance"],
    shelf: "TBR",
  },

  {
    title: "Everything I Know About Love",
    author: "Dolly Alderton",
    description: "A candid memoir about growing up, navigating relationships and hearTBReak, and discovering the enduring power of friendship.",
    image: "book_2.jpg",
    chips: ["Autobiography", "Memoir"],
    shelf: "Read",
  },
  {
    title: "Atomic Habits",
    author: "James Clear",
    description: "A practical guide showing how small daily habits can compound into remarkable personal and professional growth.",
    image: "book_13.jpg",
    chips: ["Self Improvement", "Productivity"],
    shelf: "Read",
  },
  {
    title: "Dune",
    author: "Frank Herbert",
    description: "An epic science fiction saga about politics, religion, ecology, and power on the desert planet Arrakis.",
    image: "book_14.jpg",
    chips: ["Science Fiction", "Epic"],
    shelf: "Read",
  },
  {
    title: "The Hunger Games",
    author: "Suzanne Collins",
    description: "Katniss Everdeen volunteers for a deadly televised competition where only one tribute can survive.",
    image: "book_15.jpg",
    chips: ["Dystopian", "Adventure"],
    shelf: "Read",
  },
  {
    title: "The Alchemist",
    author: "Paulo Coelho",
    description: "A shepherd boy travels the world seeking treasure and ultimately learns to follow his dreams.",
    image: "book_16.jpg",
    chips: ["Philosophy", "Adventure"],
    shelf: "Read",
  },
  {
    title: "Where the Crawdads Sing",
    author: "Delia Owens",
    description: "A haunting coming-of-age mystery set in the marshes of North Carolina.",
    image: "book_17.jpg",
    chips: ["Mystery", "Literary Fiction"],
    shelf: "Read",
  },
  {
    title: "The Seven Husbands of Evelyn Hugo",
    author: "Taylor Jenkins Reid",
    description: "A reclusive Hollywood icon recounts her glamorous and scandalous life story.",
    image: "book_18.jpg",
    chips: ["Historical Fiction", "Drama"],
    shelf: "Read",
  },
  {
    title: "The Great Gatsby",
    author: "F. Scott Fitzgerald",
    description: "A tragic story of love, ambition, and the illusion of the American dream in the roaring twenties.",
    image: "book_19.jpg",
    chips: ["Classic", "Literary Fiction"],
    shelf: "Read",
  },
  {
    title: "The Hobbit",
    author: "J.R.R. Tolkien",
    description: "Bilbo Baggins joins a quest to reclaim a dwarf kingdom from the dragon Smaug.",
    image: "book_20.jpg",
    chips: ["Fantasy", "Adventure"],
    shelf: "Read",
  },
  {
    title: "The Fault in Our Stars",
    author: "John Green",
    description: "Two teenagers with cancer meet at a support group and fall deeply in love.",
    image: "book_21.jpg",
    chips: ["Romance", "Young Adult"],
    shelf: "Read",
  },
  {
    title: "Educated",
    author: "Tara Westover",
    description: "A memoir about a woman who leaves her survivalist family and pursues education.",
    image: "book_22.png",
    chips: ["Memoir", "Inspiration"],
    shelf: "Read",
  },
  {
    title: "Circe",
    author: "Madeline Miller",
    description: "A retelling of the mythological witch Circe as she discovers her power and identity.",
    image: "book_23.jpg",
    chips: ["Fantasy", "Mythology"],
    shelf: "Read",
  },

  {
    title: "A Tree Grows in Brooklyn",
    author: "Betty Smith",
    description: "This novel follows Francie Nolan’s coming-of-age in early 1900s Brooklyn as she endures poverty with resilience and hope.",
    image: "book_3.jpg",
    chips: ["Coming of Age", "Historical Fiction"],
    shelf: "Reading",
  },
  {
    title: "Akin",
    author: "Emma Donoghue",
    description: "A retired professor travels to France with his young great-nephew and uncovers long-hidden family secrets.",
    image: "book_4.jpg",
    chips: ["Contemporary Fiction", "Historical Fiction"],
    shelf: "Reading"
  },
  {
    title: "The Midnight Library",
    author: "Matt Haig",
    description: "A woman discovers a magical library that lets her explore the lives she could have lived.",
    image: "book_24.jpg",
    chips: ["Fantasy", "Philosophical"],
    shelf: "Reading"
  }
])

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
    <v-carousel hide-delimiter-background hide-delimiters continuous height="400" :show-arrows="false">
      <v-carousel-item
        v-for="(group, index) in ReadingChunks"
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
    <h2>Past Reads</h2>
    <v-carousel hide-delimiter-background hide-delimiters continuous height="400">
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
    <v-carousel hide-delimiter-background hide-delimiters continuous height="400">
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
        <v-chip v-for="chip in selectedBook.chips" :key="selectedBook.chip" class="chipp">
          {{ chip }}
        </v-chip>
        <v-chip class="shelfchip">
          Shelf: {{ selectedBook.shelf }}
        </v-chip> <br> <br>
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
.shelfchip {
  background-color: #3a3a3a;
  color: #fff;
  padding: 6px 12px;
  margin: 4px 4px 0 0;
  border-radius: 16px;
  font-size: 0.8rem;
}
</style>