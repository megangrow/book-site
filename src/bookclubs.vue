<script setup>
  import {ref} from "vue";
  import ClubCard from "./components/clubCard.vue";

  const clubs=ref([
    {
      id: 1,
      name: 'Breakfast Book Club',
      address: 'Online',
      hours: 'Tuesdays at 9am',
      image: 'breakfast_club.jpg',
      tags: ['Human Behavior', 'Habits and Productivity', 'Self Improvement'],
      members: 34,
      details: [
          'Casual group',
          'Bring coffee and/or breakfast to the call',
      ],
      contact: 'Megan Grow. megan@email.com'
    },
    {
      id: 2,
      name: 'SciFi',
      address: 'Public Library: 340 Main St, Milwaukee, WI',
      hours: 'Thursdays at 7pm',
      image: 'scifi_club.jpg',
      tags: ['Science Fiction', 'Outer Space', 'Dystopia'],
      members: 63,
      details: [
        'Virtual participation option',
        'New members always welcome',
        'Themed dress-up days once a month',
      ],
      contact: 'Jeremy Smith. jerrysmi@mail.com'
    },
    {
      id: 3,
      name: 'History Enthusiasts',
      address: 'Virtual only',
      hours: 'Sundays at 12pm',
      image: 'history_club.png',
      tags: ['Biographies', 'History', 'Historical Fiction'],
      members: 8,
      details: [
        'Major history enthusiasts only',
        'Deep thinking and discussions',
      ],
      contact: 'Aaron Hunt. aahunt@email.mail.com'
    },
    {
      id: 4,
      name: 'Hopeless Romantics',
      address: 'Indie Coffee Shop, 334 West Ln, Baraboo, WI',
      hours: 'Saturdays at 2pm',
      image: 'hearts_club.png',
      tags: ['Romance', 'Romantic Comedies', 'Period Pieces'],
      members: 27,
      details: [
          'Have a cup of coffee and talk about loveee',
          'Bring a friend - new members always welcome!',
          'Romantic books exclusively',
      ],
      contact: 'Jerri Manly. jerriluv@mail.net'
    }
  ])

  const dialogOpen = ref(false)
  const selected = ref(null)

  const snackbarOpen = ref(false)
  const snackbarText = ref('')

  function openDetails(location) {
    selected.value = location
    dialogOpen.value = true
  }

  async function copyAddress(contact) {
    try {
      await navigator.clipboard.writeText(contact)
      snackbarOpen.value = true
      snackbarText.value = 'Contact information copied'
    } catch (e) {
      snackbarText.value = 'Could not auto-copy. Please copy manually.'
    }
  }
</script>

<template>
<v-container>
  <div class="hero">
      <h1>Join a Virtual Book Club!</h1>
      <p>Browse the following public clubs to find one that fits your vibe!</p>
  </div>

  <v-carousel hide-delimiter-background continuous height="500">
    <v-carousel-item v-for="club in clubs" :key="club.id">
      <div class="d-flex justify-center">
      <ClubCard
          :hours="club.hours"
          :address="club.address"
          :members="club.members"
          :name="club.name"
          :image="club.image"
          :tags="club.tags"
          @view-details="openDetails(club)"
          @contact="copyAddress(club.contact)"

      ></ClubCard>
      </div>
    </v-carousel-item>
  </v-carousel>


<!--  Details Popup  -->
  <v-dialog v-model="dialogOpen" max-width="650">
    <v-card v-if="selected">
      <v-img :src="selected.image" height="220" cover></v-img>
      <v-card-title class="club-title">{{selected.name}}</v-card-title>
      <v-card-subtitle class="pb-0 club-card">{{selected.address}} - {{selected.members}} members</v-card-subtitle>

      <v-card-text class="pt-4 club-card">
        <v-alert variant="tonal" icon="mdi-clock-time-eight-outline" class="mb-4" :text="`When we meet: ${selected.hours}`"/>
        <h3 class="mb-2">Our favorite genres: </h3>
        <div class="mb-3" style="padding-top: 3px">
        <v-chip v-for="tag in selected.tags" :key="tag" class="mr-2 mb-2" variant="tonal">
          {{tag}}
        </v-chip>
        </div>

        <v-divider class="mb-4"></v-divider>
        <h3 class="mb-2">About the club:</h3>
        <v-list density="compact">
          <v-list-item v-for="(line, i) in selected.details" :key="i" prepend-icon="mdi-book-heart">
            <v-list-item-title>{{line}}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-card-text>
      <v-card-actions>
        <v-btn variant="tonal" @click="copyAddress(selected.contact)">
          <v-icon start>mdi-card-account-mail</v-icon>
          Contact {{ selected.contact }} to Join
        </v-btn>
        <v-spacer/>
        <v-btn variant="flat" color="pink-darken-2" @click="dialogOpen=false">
          Close
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>

<v-snackbar v-model="snackbarOpen" timeout="1800">
  {{ snackbarText }}
  <template #actions>
    <v-btn variant="text" @click="snackbarOpen = false">Dismiss</v-btn>
  </template>
</v-snackbar>
</v-container>
</template>

<style scoped>

</style>