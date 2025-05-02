<template>
  <button class="button" :type="type">
    <slot/>
  </button>
</template>

<script setup>
const props = defineProps({
  type:
      {
        type: String,
        default: 'button',
      },
});
</script>

<style>
.button {
  font-size: 24px;
  color: var(--color-white);
  font-weight: 400;
  text-align: center;
  background-color: var(--color-primary);
  cursor: pointer;
  border: none;
  border-radius: 100px;
  padding: 20px 91px;
}

.button:hover {
  background-color: var(--color-primary-hover);
}
</style>