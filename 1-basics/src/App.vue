<template>
  <div class="wrapper">
    <Header :score="score"/>
    <div class="content">
      <Card
          v-for="card of cards"
          :isTurnCard="isTurnCard"
          :state="card.state"
          :status="card.status"
          :translation="card.translation"
          :word="card.word"
          @add-action="addAction"
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
import {ref} from "vue";

const score = ref(0);
const isTurnCard = ref(false);
const cards = ref([{
  word: 'En word',
  translation: 'Ru word',
  state: 'close',
  status: 'success'
}]);

const addAction = (isAnswer) => {
  score.value = isAnswer ? ++score.value : --score.value;
  isTurnCard.value = false;
}

const turnCard = () => {
  isTurnCard.value = true;
}
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
