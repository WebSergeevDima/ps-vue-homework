<template>
  <div class="card">
    <div class="content">
      <div class="count">01</div>
      <div class="word">Слово</div>
      <div class="action" v-if="props.isTurnCard">
        <IconNo @click="emit('addAction', false)" />
        <IconYes @click="emit('addAction', true)" />
      </div>
      <div class="action" @click="emit('turnCard')" v-if="!props.isTurnCard">
        Перевернуть
      </div>
    </div>
  </div>
</template>

<script setup>
import IconYes from "../../icons/IconYes.vue";
import IconNo from "../../icons/IconNo.vue";

const emit = defineEmits(['addAction', 'turnCard']);
const props = defineProps({
  isTurnCard: {
    type: Boolean,
    default: false
  }
})
</script>

<style scoped>
.card {
  width: 250px;
  height: 376px;
  padding: 15px;
}

.content {
  border: 1px var(--bg-primary) solid;
  border-radius: 12px;
  position: relative;
  height: 100%;
}

.count {
  font-size: 14px;
  font-weight: 400;
  position: absolute;
  top: -9px;
  left: 17px;
  background-color: var(--color-white);
  padding: 0 3px;
}

.action {
  text-transform: uppercase;
  font-size: 12px;
  font-weight: 700;
  position: absolute;
  bottom: -8px;
  left: 50%;
  transform: translateX(-50%);
  background-color: var(--color-white);
  padding: 0 5px;
  min-width: 85px;
  display: flex;
  justify-content: space-between;
}

.word {
  position: absolute;
  top: 50%;
  transform: translateY(-50%) translateX(-50%);
  left: 50%;
  font-weight: 400;
  font-size: 18px;
}
</style>