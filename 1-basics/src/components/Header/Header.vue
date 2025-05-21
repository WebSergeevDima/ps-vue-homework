<template>
  <header class="header">
    <div class="title">Запомни слово</div>
    <Score :score="props.score" />
  </header>
</template>

<script setup>
import Score from "../Score/Score.vue";

const props = defineProps({
  score: {
    type: Number,
    default: 0
  }
})
</script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100px;
  padding: 20px;
}

.title {
  font-size: 16px;
  font-weight: 700;
  text-transform: uppercase;
}
</style>