<template>
<div class="wrapper">
  <Header :score="score" />
  <div class="content">
    <Card @add-action="addAction" @turn-card="turnCard" />
    <Button type="button">Начать игру</Button>
  </div>
</div>
</template>

<script setup>
import Button from './components/Button/Button.vue';
import Header from "./components/Header/Header.vue";
import Card from "./components/Card/Card.vue";

const score = 100;

const addAction = (isAnswer) => {
  console.log('isAnswer: ', isAnswer)
}

const turnCard = () => {
  console.log('turnCard! ')
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
