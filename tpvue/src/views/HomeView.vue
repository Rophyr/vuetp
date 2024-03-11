<template>
  <div>
    <h1>Magic: The Gathering</h1>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const cards = ref([])

onMounted(async () => {
  try {
    const response = await axios.get(`https://api.magicthegathering.io/v1/cards`)
    cards.value = response.data.cards
  } catch (error) {
    console.error(error)
  }
})
</script>
