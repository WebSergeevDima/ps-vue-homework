<template>
<div class="score">
  {{ props.score}} <IconHeart />
</div>
</template>

<script setup>
import IconHeart from "../../icons/IconHeart.vue";

const props = defineProps({
  score: {
    type: Number,
    default: 0
  }
})
</script>

<style scoped>
.score {
  background-color: var(--bg-primary);
  color: var(--color-primary);
  display: flex;
  align-items: center;
  font-size: 16px;
  font-weight: 700;
  padding: 10px 15px;
  gap: 10px;
  border-radius: 36px;
}
</style>