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
      <div v-else class="cards">
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
      </div>
      <Button type="button" @click="startGame">Начать игру</Button>
    </div>
  </div>
</template>

<script setup>
import Button from './components/Button/Button.vue';
import Header from "./components/Header/Header.vue";
import Card from "./components/Card/Card.vue";
import {onMounted, ref} from "vue";

const API_RANDOM_WORDS = 'http://localhost:8080/api/random-words';

const score = ref(0);
const isTurnCard = ref(false);
const isLoading = ref(false);
const error = ref(null);

const cards = ref([]);

const updateScore = (isAnswer) => {
  score.value += isAnswer ? 1 : -1;
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

onMounted(startGame);
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
  align-items: center;
  justify-content: center;
  height: calc(100vh - 100px);
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