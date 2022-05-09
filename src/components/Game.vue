<script setup lang="ts">
import { ref, computed } from "vue";
import Board from "./Board.vue";

let isNextPlayerX = ref(true)
const stepNumber = ref(0)
const history = ref([{ squareList: new Array(9).fill(null) }])
const handleClick = (index: number): void => {
  const copyHistory = history.value.slice(0, stepNumber.value + 1)
  const current = copyHistory[copyHistory.length - 1].squareList.slice()
  if (current[index] || calcWinner(current)) return
  current[index] = isNextPlayerX.value ? 'X' : 'O'
  isNextPlayerX.value = !isNextPlayerX.value
  history.value = copyHistory.concat([{ squareList: current }])
  stepNumber.value++
}
const calcWinner = (arr: Array<string | null>) => {
  const winRes = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  for (let i = 0; i < winRes.length; i++) {
    const [a, b, c] = winRes[i];
    if (arr[a] && arr[a] === arr[b] && arr[a] === arr[c]) {
      return arr[a];
    }
  }
  return null;
}
const calcTip = computed(() => {
  const winner = calcWinner(history.value[stepNumber.value].squareList)
  if (winner) {
    return 'Winner: ' + winner
  } else {
    return 'The next Player: ' + (isNextPlayerX.value ? 'X' : 'O')
  }
})
const jumpTo = (index: number): void => {
  stepNumber.value = index
  isNextPlayerX.value = index % 2 ? false : true
}
</script>

<template>
  <div class="game">
    <Board @handleClick="handleClick" :squareList="history[stepNumber].squareList" />
    <div class="game-info">
      <span>{{ calcTip }}</span>
      <ol>
        <li v-for="(item, index) in history" :key="index">
          <button @click="jumpTo(index)">{{ index ? 'Go to move #' + index : 'Go to game start' }}</button>
        </li>
      </ol>
    </div>
  </div>
</template>

<style scoped>
.game {
  display: flex;
}

.game-info {
  margin-left: 30px;
}
</style>
