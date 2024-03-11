<template>
  <div class="navbar">
    <router-link class="nav-link" to="/">Home</router-link>
    <router-link class="nav-link" to="/cards">Cartes</router-link>
    <input type="text" v-model="searchQuery" @input="searchCards" placeholder="Rechercher une carte par son nom">
    <CardList :cards="filteredCards" />
    <SetList :sets="sets" />
  </div>
</template>

<script setup>
import { onMounted, ref, computed } from 'vue'
import axios from 'axios'
import CardList from './components/CardList.vue'
import SetList from './components/SetList.vue'

const cards = ref([])
const sets = ref([])
const searchQuery = ref('')

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

const filteredCards = computed(() => {
  if (!searchQuery.value) {
    return cards.value
  } else {
    const searchTerm = searchQuery.value.trim().toLowerCase()
    return cards.value.filter(card => card.name.toLowerCase().includes(searchTerm))
  }
})

function searchCards() {
  // Pas besoin de faire quelque chose ici, la recherche se fait automatiquement grâce à computed
}
</script>
