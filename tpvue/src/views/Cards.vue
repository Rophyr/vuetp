<template>
  <div>
    <CardList :cards="cards" />
    <SetList :sets="sets" />
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import CardList from '../components/CardList.vue'
import SetList from '../components/SetList.vue'

const cards = ref([])
const sets = ref([])

onMounted(async () => {
  try {
    const responseCards = await axios.get(`https://api.magicthegathering.io/v1/cards`)
    cards.value = responseCards.data.cards

    const responseSets = await axios.get(`https://api.magicthegathering.io/v1/sets`)
    sets.value = responseSets.data.sets
  } catch (error) {
    console.error(error)
  }
})
</script>
