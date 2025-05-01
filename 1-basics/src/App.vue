<script setup>
const date = new Date().toLocaleDateString('ru-RU', {
  year: "numeric",
  month: "2-digit",
  day: "2-digit",
  hour: "2-digit",
  minute: "2-digit"
})
</script>

<template>
  <h1>Дата: <span class="red">{{ date }}</span></h1>
</template>

<style scoped>
.red {
  color: red;
}
</style>
