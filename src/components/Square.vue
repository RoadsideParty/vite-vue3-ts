<script setup lang="ts">
import { defineEmits, defineProps } from 'vue'
defineProps(['value'])

const emits = defineEmits(['clickSquare'])
const clickSquare = (): void => {
  emits('clickSquare')
}
</script>

<template>
  <div class="square" @click="clickSquare">{{ value }}</div>
</template>

<style scoped>
.square {
  border: 1px solid black;
  cursor: pointer;
  line-height: 100px;
  text-align: center;
  font-size: 50px;
  font-weight: bold;
}
</style>
