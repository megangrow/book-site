<script setup>
import { ref, computed } from "vue"
import SectionHeader from "./components/sectionHeader.vue"
import OrderForm from "./components/orderForm.vue"
import OrderSummary from "./components/orderSummary.vue"
import ConfirmDialog from "./components/confirmDialog.vue"

const menu = [
  { id: 1, name: "Classic Lemonade", price: 2 },
  { id: 2, name: "Strawberry Lemonade", price: 3 },
]

const locations = ["Downtown", "Park", "Market"]

const order = ref({
  customerName: "",
  email: "",
  location: null,
  items: [],
  sweetness: 50,
  agree: false,
})

const dialogOpen = ref(false)
const snackbarOpen = ref(false)
const snackbarText = ref("")

function openConfirm() {
  dialogOpen.value = true
}

function confirmOrder() {
  dialogOpen.value = false
  snackbarText.value = "Order submitted!"
  snackbarOpen.value = true
}
</script>

<template>
  <v-container>
    <SectionHeader title="Place an Order" />

    <v-row>
      <v-col cols="12" md="8">
        <OrderForm
            v-model:order="order"
            :menu="menu"
            :locations="locations"
            @submit="openConfirm"
        />
      </v-col>

      <v-col cols="12" md="4">
        <OrderSummary :order="order" :menu="menu" />
      </v-col>
    </v-row>

    <ConfirmDialog
        v-model:open="dialogOpen"
        :order="order"
        :menu="menu"
        @confirm="confirmOrder"
    />
  </v-container>
</template>