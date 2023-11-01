 
<script setup lang="ts">
import { ref } from 'vue';
import { checkWinnerFrom, checkEndGame } from "../services/board.js";
import { TURNS } from '../constants.js';
import Square from '../components/Square.vue';

const board = ref(Array(9).fill(null));
const winner = ref(null);
const turn = ref(TURNS.X);
const canPlay = ref(true);

const resetGame = () => {
    board.value = Array(9).fill(null);
    turn.value = TURNS.X;
    winner.value = null;
    canPlay.value = true;
};

const updateBoard = (index: number) => {
    if (board.value[index] || winner.value || !canPlay.value) return;

    const newBoard = [...board.value];
    newBoard[index] = turn.value;
    board.value = newBoard;

    const newTurn = turn.value === TURNS.X ? TURNS.O : TURNS.X;
    turn.value = newTurn;

    const newWinner = checkWinnerFrom(newBoard);
    if (newWinner) {
        winner.value = newWinner;
    } else if (checkEndGame(newBoard)) {
        // @ts-ignore
        winner.value = false;
    }
};
</script>
  

<template>
    <div class="font-sans bg-[#0D0F12] h-screen flex flex-col items-center justify-center gap-20 relative">
        <h1 class="text-7xl font-extrabold text-[#E3E6E8]">Tic Tac Toe</h1>
        <div class="grid grid-cols-3">
            <Square v-for="(square, index) in board" :key="index" :index="index" :updateBoard="updateBoard">
                <img v-if="square === 'X'" class="w-3/5" src="/cross.png" width="100" height="100" alt="cross" />
                <img v-if="square === 'O'" class="w-3/5 invert" src="/circle.png" width="100" height="100" alt="circle" />
            </Square>
        </div>
        <div v-if="winner === null" class="absolute bottom-10 right-10 flex flex-col items-center justify-center gap-2">
            <span class="text-[#999] font-semibold text-lg">Current turn</span>
            <div class="grid place-items-center">
                <img v-if="turn === 'X'" class="" src="/cross.png" width="100" height="100" alt="cross" />
                <img v-if="turn === 'O'" class="invert" src="/circle.png" width="100" height="100" alt="circle" />
            </div>
        </div>
    </div>
</template>
