<script setup>
import { ref } from "vue"

const props = defineProps({
  order: Object,
  menu: Array,
  locations: Array,
})

const emit = defineEmits(["update:order","submit"])

const step = ref(1)
const formContact = ref(null)

function setField(key,value){
  emit("update:order",{...props.order,[key]:value})
}

async function next(){
  const r = await formContact.value.validate()
  if(r.valid) step.value=2
}
</script>

<template>
  <v-stepper v-model="step">
    <v-stepper-header>
      <v-stepper-item :value="1" title="Contact"/>
      <v-stepper-item :value="2" title="Order"/>
    </v-stepper-header>

    <v-stepper-window>
      <v-stepper-window-item :value="1">
        <v-form ref="formContact">
          <v-text-field
              :model-value="order.customerName"
              @update:model-value="v=>setField('customerName',v)"
              label="Name"
          />
          <v-btn @click="next">Next</v-btn>
        </v-form>
      </v-stepper-window-item>

      <v-stepper-window-item :value="2">
        <v-select
            :items="menu"
            item-title="name"
            item-value="id"
            multiple
            :model-value="order.items"
            @update:model-value="v=>setField('items',v)"
        />

        <v-btn @click="$emit('submit')">
          Review & Submit
        </v-btn>
      </v-stepper-window-item>

    </v-stepper-window>
  </v-stepper>
</template>