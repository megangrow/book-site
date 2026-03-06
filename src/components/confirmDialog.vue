<script setup>
const props = defineProps({
  open:Boolean,
  order:Object
})

const emit = defineEmits(["update:open","confirm"])
</script>

<template>
  <v-dialog
      :model-value="open"
      @update:model-value="v=>emit('update:open',v)"
  >
    <v-card>
      <v-card-title>Confirm Order</v-card-title>

      <v-card-actions>
        <v-btn @click="emit('confirm')">Confirm</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>