<template>
  <header class="header">
    <div class="title">Запомни слово</div>
    <Score />
  </header>
</template>

<script setup>
import Score from "../Score/Score.vue";
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