<template>
  <div class="wrapper">
    <Header :score="score"/>
    <div class="content">
      <Card
          v-for="card of cards"
          :key="card.word"
          :is-turn-card="isTurnCard"
          :state="card.state"
          :status="card.status"
          :translation="card.translation"
          :word="card.word"
          @add-action="updateScore"
          @turn-card="turnCard"
      />
      <Button type="button">Начать игру</Button>
    </div>
  </div>
</template>

<script setup>
import Button from './components/Button/Button.vue';
import Header from "./components/Header/Header.vue";
import Card from "./components/Card/Card.vue";
import { ref } from "vue";

const score = ref(0);
const isTurnCard = ref(false);

const cards = ref([
  {
    word: 'En word',
    translation: 'Ru word',
    state: 'closed',
    status: 'pending'
  },
  {
    word: 'En word 2',
    translation: 'Ru word 2',
    state: 'closed',
    status: 'pending'
  },
  {
    word: 'En word 2',
    translation: 'Ru word 2',
    state: 'closed',
    status: 'success'
  },
  {
    word: 'En word 3',
    translation: 'Ru word 3',
    state: 'closed',
    status: 'fail'
  }
]);

const updateScore = (isAnswer) => {
  score.value += isAnswer ? 1 : -1;
  isTurnCard.value = false;
};

const turnCard = () => {
  isTurnCard.value = true;
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
}

.header {
  height: 100px;
}

.content {
  display: flex;
  align-items: center;
  justify-content: center;
  height: calc(100vh - 100px);
}
</style>