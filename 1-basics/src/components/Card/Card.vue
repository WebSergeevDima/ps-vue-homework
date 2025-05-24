<template>
  <div class="card">
    <div class="content">
      <div class="count">01</div>
      <div class="word">Слово</div>
      <div class="status" v-if="props.status === 'success'">
        <IconYes/>
      </div>
      <div class="status" v-if="props.status === 'fail'">
        <IconNo/>
      </div>
      <div class="actionBtns" v-if="props.isTurnCard && props.status === 'pending'">
        <IconNo @click="handleAction(false)" class="btn"/>
        <IconYes @click="handleAction(true)" class="btn"/>
      </div>
      <div
          class="actionTurn"
          @click="emit('turnCard')"
          v-if="!props.isTurnCard && props.status === 'pending'"
      >
        Перевернуть
      </div>
    </div>
  </div>
</template>

<script setup>
import IconYes from "../../icons/IconYes.vue";
import IconNo from "../../icons/IconNo.vue";
import {defineProps, defineEmits} from "vue";

const props = defineProps({
  isTurnCard: {
    type: Boolean,
    default: false
  },
  state: {
    type: String,
    required: true,
    validator: value => ['closed', 'opened'].includes(value)
  },
  status: {
    type: String,
    required: true,
    validator: value => ['success', 'fail', 'pending'].includes(value)
  },
  translation: {
    type: String,
    required: true
  },
  word: {
    type: String,
    required: true
  }
});

const emit = defineEmits(['addAction', 'turnCard']);

const handleAction = (isAnswer) => {
  emit('addAction', isAnswer);
};
</script>

<style scoped>
.card {
  width: 250px;
  height: 376px;
  padding: 15px;
  box-shadow: 0 0 16px 0 #0000001A;
  border-radius: 16px;
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
  z-index: 1;
}

.word {
  position: absolute;
  top: 50%;
  transform: translateY(-50%) translateX(-50%);
  left: 50%;
  font-weight: 400;
  font-size: 18px;
}

.status {
  position: absolute;
  top: -8px;
  left: 50%;
  transform: translateX(-50%) scale(1.5);
  width: 40px;
  z-index: 1;
}

.btn {
  cursor: pointer;
}

.actionBtns {
  transform: translate(-50%, -50%);
  background-color: var(--color-white);
  padding: 0 5px;
  min-width: 85px;
  display: flex;
  justify-content: space-between;
  z-index: 1;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: 700;
  position: absolute;
  bottom: -20px;
  left: 50%;
}

.actionTurn {
  transform: translate(-50%, -50%);
  background-color: var(--color-white);
  padding: 0 5px;
  min-width: 85px;
  z-index: 1;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: 700;
  position: absolute;
  bottom: -14px;
  left: 50%;
}
</style>