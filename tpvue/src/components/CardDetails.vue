<template>
  <div>
    <h2>{{ card.name }}</h2>
    <p>Set: {{ card.set }}</p>
    <p>Type: {{ card.type }}</p>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue'
import axios from 'axios'

export default {
  setup() {
    const card = ref(null)

    onMounted(async () => {
      try {
        const response = await axios.get(`https://api.magicthegathering.io/v1/cards/${$route.params.id}`)
        card.value = response.data.card
      } catch (error) {
        console.error(error)
      }
    })

    return { card }
  }
}
</script>
