<template>
  <div>
    <h2>Cartes</h2>
    <div class="card-grid">
      <div v-for="card in displayedCards" :key="card.id" class="card-item">
        <router-link :to="{ name: 'CardDetails', params: { id: card.id } }">
          <img :src="card.imageUrl" :alt="card.name" class="card-image">
          <p class="card-name">{{ card.name }}</p>
        </router-link>
      </div>
    </div>
    <div class="pagination">
      <button @click="previousPage" :disabled="currentPage === 1">Précédent</button>
      <button @click="nextPage" :disabled="currentPage === totalPages">Suivant</button>
    </div>
  </div>
</template>

<style scoped>
.card-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

.card-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.card-image {
  width: 100px;
  height: auto;
}

.card-name {
  margin-top: 10px;
}
</style>

<script>
export default {
  props: {
    cards: Array
  },
  data() {
    return {
      itemsPerPage: 100,
      currentPage: 1
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.cards.length / this.itemsPerPage);
    },
    displayedCards() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.cards.slice(startIndex, endIndex);
    }
  },
  methods: {
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    }
  }
};
</script>
