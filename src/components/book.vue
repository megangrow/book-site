<script setup>
const props = defineProps({
  title: { type: String, required: true },
  author: { type: String, required: true },
  image: { type: String, required: true },
  description: { type: String, required: true },
})

const emit = defineEmits(['view-details'])

// wrapper function for clarity
function handleViewDetails() {
  emit('view-details')
}
</script>

<template>
  <v-card class="book-card" width="160" elevation="4">
    <v-img
        :src="image"
        height="200"
        cover
        class="book-image"
    />
    <v-card-title class="book-title">
      {{ title }}
    </v-card-title>
    <v-card-subtitle class="book-author">
      {{ author }}
    </v-card-subtitle>

    <v-card-actions>
      <v-btn variant="tonal" @click="handleViewDetails">
        <v-icon start>mdi-information-outline</v-icon>
        Details
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<style scoped>
.book-card {
  border-radius: 12px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #f9f9f9;
}

.book-image {
  width: 100%;
  border-bottom: 1px solid #ddd;
}

.book-title {
  font-weight: 600;
  font-size: 0.9rem;
  text-align: center;
  margin-top: 8px;
  margin-bottom: 4px;
  min-height: auto; /* remove fixed min-height so it can grow */
  line-height: 1.2em;
  white-space: normal;   /* allow wrapping */
  word-break: break-word; /* wrap long words if needed */
  overflow-wrap: anywhere; /* fallback for long text */
}

.book-author {
  font-size: 0.8rem;
  text-align: center;
  color: #555;
  margin-bottom: 8px;
}
</style>