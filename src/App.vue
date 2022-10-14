<template>
  <div class="flex flex-col justify-center pt-8 text-center bg-gray-800 min-h-screen text-white">
    <h1 class="mb-1 text-3xl font-bold">井字棋</h1>
    <h2 class="mb-6">Tic Tac Toe</h2>
    <h3 class="text-xl mb-10">輪到 {{ player }} 玩家</h3>
    <div class="flex flex-col items-center mb-8">
      <div v-for="(row, x) in board" :key="x" class="flex">
        <div v-for="(cell, y) in row" :key="y" @click="gameStep(x, y)" :class="`flex justify-center items-center border border-white w-20 h-20 hover:bg-gray-700 material-icons-outlined text-4xl cursor-pointer ${cell === 'X'?'text-pink-500':'text-blue-500'}`">
        {{cell === 'X'?'close':cell === 'O'?'circle':''}}
      </div>
      </div>
    </div>
    <div>
      <h2 v-if="winner" class="text-5xl font-bold mb-8">玩家 {{winner}} 贏了</h2>
      <button @click="resetGame" class="px-4 py-2 bg-pink-500 rounded font-bold">
        重置遊戲
      </button>
    </div>
  </div>
</template>
<script setup>
import { ref, computed } from 'vue'
const player = ref('X')
const board = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', '']
])
const calculateWinner = (board) => {
  // 勝利規則
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ]
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i]
    // 檢測傳進來的參數陣列該相應位置的內容是否相同
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a]
    }
  }
  return null
}
const winner = computed(() => {
  console.log(calculateWinner(board.value.flat()))
  return calculateWinner(board.value.flat())
})
const gameStep = (x, y) => {
  if (winner.value) {

  } else if (board.value[x][y] !== '') {

  } else {
    board.value[x][y] = player.value
    player.value = player.value === 'X' ? 'O' : 'X'
  }
}
const resetGame = () => {
  board.value = [
    ['', '', ''],
    ['', '', ''],
    ['', '', '']
  ]
  player.value = 'X'
}
</script>
<style>

</style>
