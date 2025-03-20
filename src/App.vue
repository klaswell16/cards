<template>
  <div class="grid">
    <div
      v-for="card in cards"
      :key="card.id"
      class="flip-card"
      :class="{ flipped: card.isFlipped }"
      @click="flipCard(card)"
    >
      <div class="flip-card-inner">
        <div class="flip-card-front">
          <Card>
            <template #content>
              <p>{{ card.front }}</p>
            </template>
          </Card>
        </div>
        <div class="flip-card-back">
          <Card>
            <template #content>
              <img :src="card.back" :alt="`Card ${card.id} Back`" class="card-image" />
            </template>
          </Card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Card from 'primevue/card';

export default {
  components: {
    Card,
  },
  data() {
    return {
      cards: [
        { id: 1, front: 'Card 1 Front', back: 'src/assets/apple.webp' },
        { id: 2, front: 'Card 2 Front', back: 'src/assets/grapes.jpg' },
        { id: 3, front: 'Card 3 Front', back: 'src/assets/apple.webp' },
        { id: 4, front: 'Card 4 Front', back: 'src/assets/banana.png' },
        { id: 5, front: 'Card 5 Front', back: 'src/assets/pineapple.jpg' },
        { id: 6, front: 'Card 6 Front', back: 'src/assets/banana.png' },
        { id: 7, front: 'Card 7 Front', back: 'src/assets/grapes.jpg' },
        { id: 8, front: 'Card 8 Front', back: 'src/assets/pineapple.jpg' },
      ].map((card) => ({ ...card, isFlipped: false })),
    };
  },
  methods: {
    flipCard(card) {
      card.isFlipped = !card.isFlipped;
    },
  },
};
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  padding: 16px;
}

.flip-card {
  background-color: transparent;
  width: 150px;
  height: 200px;
  perspective: 1000px;
  cursor: pointer;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.flip-card.flipped .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.flip-card-front {
  background-color: #fff;
}

.flip-card-back {
  background-color: #f0f0f0;
  transform: rotateY(180deg);
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 8px;
}
</style>