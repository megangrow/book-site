<script setup>
const highlights = [
  {
    title: "The Martian",
    author: "Andy Weir",
    description: "The Martian follows astronaut Mark Watney as he uses science, ingenuity, and humor to survive alone on Mars after being mistakenly left behind by his crew.",
    image: "book_1.jpg",
    chips: ["Science Fiction", "Adventure"],
    added: false,
  },
  {
    title: "Everything I Know About Love",
    author: "Dolly Alderton",
    description: "A candid memoir about growing up, navigating relationships and heartbreak, and ultimately discovering that friendship is the most enduring form of love.",
    image: "book_2.jpg",
    chips: ["Autobiography", "Memoir"],
    added: false,
  },
  {
    title: "A Tree Grows in Brooklyn",
    author: "Betty Smith",
    description: "This novel follows Francie Nolan’s coming-of-age in early 1900s Brooklyn as she endures poverty with resilience, finding hope.",
    image: "book_3.jpg",
    chips: ["Coming of Age", "Historical Fiction"],
    added: true,
  },
]

const currents = [
  {
    title: "Akin",
    author: "Emma Donaghue",
    description: "A tale of love, loss and family, in which a retired New York professor's life is thrown into chaos when he takes his great-nephew to the French Riviera.",
    image: "book_4.jpg",
    chips: ["Contemporary Fiction", "Historical Fiction"],
    added: true,
    stars: 3,
    favorite: false,
  },
  {
    title: "A Tree Grows in Brooklyn",
    author: "Betty Smith",
    description: "This novel follows Francie Nolan’s coming-of-age in early 1900s Brooklyn as she endures poverty with resilience, finding hope.",
    image: "book_3.jpg",
    chips: ["Coming of Age", "Historical Fiction"],
    added: true,
    stars: 4,
    favorite: true,
  },
]
</script>

<template>
  <div class="hero">
    <h1>Currently Reading</h1>
    <p>Add what you're reading right now! Make sure to leave a review for your friends.</p>
  </div>

  <v-card class="book-card" v-for="item in currents" :key="item.title" cols="12" sm="6" md="4">
    <div v-if="item.favorite" class="top-banner">
      <v-icon>mdi-heart-circle</v-icon>
      February Favorite
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
        <v-chip v-if="item.added" class="my-shelf-chip"> My Shelf </v-chip>
        <v-chip v-for="chip in item.chips" :key="item.chip">{{ chip }}</v-chip>
      </div>
    </v-col>

    <v-col cols="3" class="ratings">
      <p border="sm">
        <v-icon v-for="star in item.stars">mdi-star</v-icon>
      </p>
      <v-btn small class="add-btn mt-2">
        Leave a Rating!
      </v-btn>
    </v-col>
    </v-row>
  </v-card>

  <div class="hero">
    <h1>Featured Books of February</h1>
    <p>Books that our shelf scouts found profound this month. </p>
  </div>
  <v-container class="mt-8">
    <v-row>
      <v-col v-for="item in highlights" :key="item.title" cols="12" sm="6" md="4">

        <v-card class="book-card" border="sm">
          <v-img :src="item.image" height="220" cover/>
          <v-card-title>{{ item.title }}</v-card-title>
          <v-card-subtitle>{{ item.author }}</v-card-subtitle>
          <v-card-text>{{ item.description }}</v-card-text>

          <div class="chips">
            <v-chip v-for="chip in item.chips" :key="item.chip">
              {{ chip }}
            </v-chip>
          </div>

          <v-card-actions class="justify-center">
            <v-btn v-if="item.added" class="add-btn">
              <v-icon start>mdi-bookshelf</v-icon>
              Added To My Shelf
            </v-btn>
            <v-btn v-else variant="tonal" class="add-btn">
              <v-icon start>mdi-bookshelf</v-icon>
              Add To My Shelf
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>

</template>

<style scoped>
.hero {
  margin-top: 2.5rem;
  margin-bottom: 2.5rem;
  text-align: center;
}

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

.add-btn {
  font-family: 'Roboto Condensed', sans-serif;
  font-weight: 700;
  text-transform: none;
  align-self: center;
  margin: 1.5rem;
}
.ratings {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
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
  background-color: #ff4081;
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