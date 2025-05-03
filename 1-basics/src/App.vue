<template>
<div class="wrapper">
  <Header :score="score" />
  <div class="content">
    <Card @add-action="addAction" @turn-card="turnCard" :isTurnCard="isTurnCard" />
    <Button type="button">Начать игру</Button>
  </div>
</div>
</template>

<script setup>
import Button from './components/Button/Button.vue';
import Header from "./components/Header/Header.vue";
import Card from "./components/Card/Card.vue";
import {ref} from "vue";

const score = ref(100);
const isTurnCard = ref(false);

const addAction = (isAnswer) => {
  console.log('isAnswer: ', isAnswer)
  score.value = score.value + 1;
  isTurnCard.value = false;
}

const turnCard = () => {
  console.log('turnCard! ')
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
