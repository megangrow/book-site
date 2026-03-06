<script setup>
import { computed } from "vue"

const props = defineProps({
  order:Object,
  menu:Array
})

const items = computed(()=>
    props.menu.filter(m=>props.order.items.includes(m.id))
)
</script>

<template>
  <v-card>
    <v-card-title>Summary</v-card-title>

    <v-list>
      <v-list-item
          v-for="i in items"
          :key="i.id"
          :title="i.name"
      />
    </v-list>

  </v-card>
</template>