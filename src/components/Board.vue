<script setup lang="ts">
import { defineEmits, defineProps } from "vue";
import Square from "./Square.vue";
defineProps({
  squareList: {
    required: true,
    type: Array
  }
})

const emits = defineEmits(['handleClick'])
const handleClick = (index: number): void => {
  emits('handleClick', index)
}
</script>

<template>
  <div class="board">
    <Square v-for="(item, index) in squareList" :key="index" :value="item" @clickSquare="handleClick(index)" />
  </div>
</template>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
}
</style>
