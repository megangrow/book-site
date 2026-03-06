<script setup>
const props = defineProps({
  name: {type: String, required: true},
  address: {type: String, required: true},
  hours: {type: String, required: true},
  image: {type: String, default: ''},
  tags: {type: Array, default: () => []},
  members: {type: String, required: true},
})

const emit = defineEmits(['view-details', 'contact'])
</script>

<template>
  <v-card class="h-200" width="660px" style="border-radius: 14px">
    <v-img v-if="image" :src="image" height="170" cover/>

    <v-card-title class="club-title">{{ name }}</v-card-title>
    <v-card-subtitle>{{ hours }}</v-card-subtitle>
    <v-card-text class="club-card">
      <div class="text-body-2 mb-3 club-card">
        <v-chip class="club-card mr-2 mb-2 chipp">
        <v-icon size="small" class="mr-1">mdi-map-marker</v-icon>
        {{ address }}
        </v-chip>
        <v-chip class="club-card mr-2 mb-2 chipp">
        <v-icon size="small" class="mr-1">mdi-account-multiple</v-icon>
        {{   members }} Members
        </v-chip>
      </div>

    </v-card-text>
    <v-card-actions>
      <v-btn variant="tonal" @click="emit('view-details')">
        <v-icon start>mdi-information-outline</v-icon>
        Details
      </v-btn>
      <v-btn variant="text" @click="emit('contact')">
        <v-icon start>mdi-card-account-mail</v-icon>
        Contact to Join
      </v-btn>
    </v-card-actions>
  </v-card>

</template>

<style scoped>
.chipp {
  background-color: #1a2a44;
  color: #FFFFFF;
}
</style>