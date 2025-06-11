<template>
  <div class="wrapper">
    <Header :score="score"/>
    <div class="content">
      <div v-if="error" class="error">
        {{ error }}
      </div>
      <div v-else-if="isLoading" class="loading">
        Loading...
      </div>
      <div v-else-if="cards.length" class="cards">
        <Card
            v-for="(card, i) of cards"
            :key="card.word"
            :is-turn-card="isTurnCard"
            :state="card.state"
            :status="card.status"
            :translation="card.translation"
            :word="card.word"
            :index="i"
            @add-action="updateScore"
            @turn-card="turnCard"
        />
      </div>
      <Button v-if="!cards.length" type="button" @click="startGame">Начать игру</Button>
      <Button v-if="cards.length" type="button" @click="startGame">Начать заново</Button>
    </div>
  </div>
</template>

<script setup>
import Button from './components/Button/Button.vue';
import Header from "./components/Header/Header.vue";
import Card from "./components/Card/Card.vue";
import {ref} from "vue";

const API_RANDOM_WORDS = 'http://localhost:8080/api/random-words';

const score = ref(0);
const isTurnCard = ref(false);
const isLoading = ref(false);
const error = ref(null);

const cards = ref([]);

const updateScore = (isAnswer, cardIndex) => {
  score.value += isAnswer ? 10 : -4;
  cards.value[cardIndex].status = isAnswer ? 'success' : 'fail';
  isTurnCard.value = false;
};

const turnCard = () => {
  isTurnCard.value = true;
};

const startGame = async () => {
  isLoading.value = true;
  error.value = null;

  try {
    const res = await fetch(API_RANDOM_WORDS, {
      method: 'GET',
    });

    if (!res.ok) {
      throw new Error('Ошибка');
    }

    const data = await res.json();

    cards.value = data.map(item => ({
      ...item,
      state: 'closed',
      status: 'pending'
    }));
  } catch (err) {
    error.value = err.message;
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  max-width: 1500px;
  gap: 50px;
  justify-content: center;
  margin: 0 auto;
}

.content {
  display: flex;
  align-items: center;
  justify-content: center;
  height: calc(100vh - 100px);
  text-align: center;
  flex-direction: column;
  gap: 100px;
}

.error {
  color: red;
  text-align: center;
  margin: 20px 0;
}

.loading {
  text-align: center;
  margin: 20px 0;
}
</style>